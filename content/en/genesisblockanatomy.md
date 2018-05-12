---
title: Anatomy of the Slimcoin Genesis Block
codeType: analysis
menuitem: Genesis Block Anatomy
lang: en
ref: genesisblockanatomy
category: technology
layout: page
permalink: /anatomy-genesis-block/
priority: 5
---


# Anatomy of the Slimcoin genesis block

The anatomy of the Slimcoin genesis block, offered as a guide to further, more detailed analysis.

#### The raw data

The Slimcoin genesis block, in hexadecimal, as produced by `xxd`:

    6e8b92a53901000000000000000000000000000000000000000000000000000000000000000
    00000003f7583d783309170cffd19d39a5f857a14e4b91096afad21c3355d5e7d86e3ba5cdf
    6b53ffff0f1e88c801000000000000000000000000000000000000000000000000000000000
    000000000000000000000000000000000000000000000000000000000000000000000000000
    ffffffffffffffffffffffff00000000000000000000000001010000005cdf6b53010000000
    000000000000000000000000000000000000000000000000000000000ffffffff4e04ffff00
    1d020f274552543a203220736f7574686561737420556b72616e69616e20726567696f6e732
    0746f20686f6c64207265666572656e64756d204d617920313120617320706c616e6e6564ff
    ffffff010000000000000000000000000000

Normally, access to genesis block data is via the GUI or the JSON RPC API.

When the RPC API is commanded:

    > getblockhash 0
    00000766be5a4bb74c040b85a98d2ba2b433c5f4c673912b3331ea6f18d61bea
    > getblock "00000766be5a4bb74c040b85a98d2ba2b433c5f4c673912b3331ea6f18d61bea"

the Slimcoin client responds with the following rendering of the genesis block (block 0):

```json
{
  "hash" : "00000766be5a4bb74c040b85a98d2ba2b433c5f4c673912b3331ea6f18d61bea",
  "size" : 313,
  "height" : 0,
  "version" : 1,
  "merkleroot" : "bae3867d5e5d35c321adaf9610b9e4147a855f9ad319fdcf70913083d783753f",
  "time" : "2014-05-08 19:47:40 UTC",
  "nonce" : 116872,
  "bits" : "1e0fffff",
  "difficulty" : 0.00024414,
  "mint" : 0.00000000,
  "nextblockhash" : "000006e022fc5e432e55cd61885d6ab9bb2ad6d5cef943f0e397ee21fe37b5db",
  "flags" : "proof-of-work",
  "proofhash" : "00000766be5a4bb74c040b85a98d2ba2b433c5f4c673912b3331ea6f18d61bea",
  "entropybit" : 1,
  "modifier" : "0000000000000000",
  "modifierchecksum" : "0e00670b",
  "nEffectiveBurnCoins" : "0",
  "Formatted nEffectiveBurnCoins" : "0.00",
  "nBurnBits" : "00000000",
  "tx" : [
    "bae3867d5e5d35c321adaf9610b9e4147a855f9ad319fdcf70913083d783753f"
    ]
}
```

We’d like to be able to do something similar for ourselves by reading the blockchain data because, as we will see, the JSON RPC API response isn’t actually what’s been written to the blockchain.

And there are regions of the blockchain where the API cannot go, e.g. the genesis block transaction:

    > getrawtransaction "bae3867d5e5d35c321adaf9610b9e4147a855f9ad319fdcf70913083d783753f"
    error: {"code":-5,"message":"No information available about transaction"}

We want to get our hands dirty, twiddling with the actual bits and bytes of the information (and only *then* will we be on the true path to mastery).

## How Bitcoin does it

A map is needed to identify and read the encoded data

Here's an example in Python (taken from [Bitcoin Stackexchange](https://bitcoin.stackexchange.com/questions/36321/extract-genesis-block-raw-tx-data)) which communicates a clear working pattern:

```python
# Read file
# https://bitcoin.org/en/developer-reference#block-headers
# https://en.bitcoin.it/wiki/Protocol_specification#block
magic            = ds.read_bytes(4).encode('hex')
block_size       = int(ds.read_bytes(4).encode('hex'), 16)
version          = ds.read_bytes(4).encode('hex')
prev_header_hash = ds.read_bytes(32).encode('hex')
merkle_root_hash = ds.read_bytes(32).encode('hex')
timestamp        = ds.read_bytes(4).encode('hex')
nBits            = ds.read_bytes(4).encode('hex')
nonce            = ds.read_bytes(4).encode('hex')

num_of_transaction = ds.read_bytes(1).encode('hex')
tx_version         = ds.read_bytes(4).encode('hex')
tx_input           = ds.read_bytes(1).encode('hex')
tx_prev_output     = ds.read_bytes(36).encode('hex')
script_length      = ds.read_bytes(1).encode('hex')
scriptsig          = ds.read_bytes(int((script_length), 16)).encode('hex')
sequence           = ds.read_bytes(4).encode('hex')
tx_output          = ds.read_bytes(1).encode('hex')
BTC_num            = ds.read_bytes(8).encode('hex')
pk_script_len      = ds.read_bytes(1).encode('hex')
pk_script          = ds.read_bytes(int(pk_script_len, 16)).encode('hex')
lock_time          = ds.read_bytes(4).encode('hex')
```

Generally this informs us that the pattern basically involves serially calling a routine that reads a given number of bytes (e.g. `ds.read_bytes(4)`) and returning the result encoded as hexadecimal.

The above map/pattern reflects the structure of Bitcoin blocks, Slimcoin blocks are different, so we will need to adjust the map to reflect the structure of Slimcoin blocks.

## How Slimcoin does it

We can begin our derivation of a pattern specific to Slimcoin by referencing the definition embodied in the the Slimcoin C++ source code.

> The world of Bitcoin is notorious for its innovative **documentation-by-implementation** approach (aka “Use the source, Luke”) but on occasion its shades into a more contentious **specification-by-implementation** approach, hence the reason for dirty hands.)

In this instance, Simcoin’s [`main.h` header file](https://github.com/slimcoin-project/Slimcoin/blob/slimcoin/src/main.h#L1083) describes how the variables are typed.

The standard C++ datatypes are highlighted, Slimcoin-specific datatypes are not:

```c++
// header
int nVersion;
uint256 hashPrevBlock;
uint256 hashMerkleRoot;
unsigned int nTime;
unsigned int nBits;
unsigned int nNonce;

// Proof-of-Burn switch, indexes, and values
bool fProofOfBurn;
uint256 hashBurnBlock;//in case there was a fork, used to check if the burn
                      // coords point to the block intended
uint256 burnHash;     //used for DoS detection
s32int burnBlkHeight; //the height the block containing the burn tx is found
s32int burnCTx;       //the index in vtx of the burn tx
s32int burnCTxOut;    //the index in the burn tx's vout to the burnt coins output
int64 nEffectiveBurnCoins;
u32int nBurnBits;
// network and disk
std::vector<CTransaction> vtx;
// ppcoin: block signature - signed by coin base txout[0]'s owner
std::vector<unsigned char> vchBlockSig;
```


(A point to note - treatment of most of the types is relatively straightworward, with the important exception of `vtx` which is a *vector* that contains an arbitrary number of transactions, each of which must be read separately according to the respective patterns for input and output transactions.)

The Slimcoin-specific datatypes are defined in `util.h`:

```c++
typedef unsigned long long  uint64;
typedef          long long  int64;
typedef unsigned int        u32int;
typedef          int        s32int;
typedef unsigned short      u16int;
typedef          short      s16int;
typedef unsigned char       u8int;
typedef          char       s8int;
```

and the actual pattern of the data that is written to the block is precisely described in `main.h`.

### The Slimcoin difference

At this point it is useful to conduct a comparison of the [Slimcoin code](https://github.com/slimcoin-project/Slimcoin/blob/slimcoin/src/main.h#L1119) and the [PPCoin cloneparent code](https://github.com/peercoin/peercoin/blob/master/src/main.h#L909) that deals with reading/writing the block to inform ourselves of the details:

```diff
--- pp.cpp   Sun Jul  9 19:00:04 2017
+++ slm.cpp  Sun Jul  9 19:01:42 2017
@@ -7,6 +7,16 @@
         READWRITE(nTime);
         READWRITE(nBits);
         READWRITE(nNonce);
+
+        //PoB data
+        READWRITE(fProofOfBurn);
+        READWRITE(hashBurnBlock);
+        READWRITE(burnHash);
+        READWRITE(burnBlkHeight);
+        READWRITE(burnCTx);
+        READWRITE(burnCTxOut);
+        READWRITE(nEffectiveBurnCoins);
+        READWRITE(nBurnBits);
 
         // ConnectBlock depends on vtx following header to generate CDiskTxPos
         if (!(nType & (SER_GETHASH|SER_BLOCKHEADERONLY)))
```

Now we know exactly what has to be added the pattern reader in terms of bits and bytes to get it to read the proof-of-burn additions.

I have taken the liberty of adding the datatype as an end-of-line comment to make it clear that we need to map the C++ datatype to its Pythonic correlate.

```c++
IMPLEMENT_SERIALIZE
(
    READWRITE(this->nVersion); // int
    nVersion = this->nVersion; 
    READWRITE(hashPrevBlock); // uint256
    READWRITE(hashMerkleRoot); // uint256
    READWRITE(nTime); // unsigned int
    READWRITE(nBits); // unsigned int
    READWRITE(nNonce); // unsigned int

    //PoB data
    READWRITE(fProofOfBurn); // bool
    READWRITE(hashBurnBlock); // uint256
    READWRITE(burnHash); // uint256
    READWRITE(burnBlkHeight); // s32int
    READWRITE(burnCTx); // s32int
    READWRITE(burnCTxOut); // s32int
    READWRITE(nEffectiveBurnCoins); // int64
    READWRITE(nBurnBits);  // u32int

    // ConnectBlock depends on vtx following header to generate CDiskTxPos
    if (!(nType & (SER_GETHASH|SER_BLOCKHEADERONLY)))
    {
        READWRITE(vtx);
        READWRITE(vchBlockSig);
    }
    else if (fRead)
    {
        const_cast<CBlock*>(this)->vtx.clear();
        const_cast<CBlock*>(this)->vchBlockSig.clear();
    }
)
```

(Note the painpoint: `READWRITE(vtx`)

I’m mainly interested in building a basic understanding of these undocumented mint-by-proof-of-burn features and I habitually use Python for such scribbled attempts. 

We’ll need to work out the number of bytes for each of `fProofOfBurn` and friends. Fortunately, Python has a mapping we can consult :

### *Python 3.5 (stable)* 7.1. struct — Interpret bytes as packed binary data
[struct format characters](https://docs.python.org/3.5/library/struct.html#format-characters)

<table>
    <colgroup><col width="10%"><col width="32%"><col width="24%"><col width="20%"><col width="15%"></colgroup>
    <tr><td><b>Format</b></td><td><b>C Type</b></td><td><b>Python type</b></td><td><b>Standard size</b></td></tr>
    <tr><td>x</td><td>pad byte</td><td>no value</td><td></td></tr>
    <tr><td>c</td><td>char</td><td>bytes of length 1</td><td>1</td></tr>
    <tr><td>b</td><td>signed char</td><td>integer</td><td>1</td></tr>
    <tr><td>B</td><td>unsigned char</td><td>integer</td><td>1</td></tr>
    <tr><td>?</td><td>_Bool</td><td>bool</td><td>1</td></tr>
    <tr><td>h</td><td>short</td><td>integer</td><td>2</td></tr>
    <tr><td>H</td><td>unsigned short</td><td>integer</td><td>2</td></tr>
    <tr><td>i</td><td>int</td><td>integer</td><td>4</td></tr>
    <tr><td>I</td><td>unsigned int</td><td>integer</td><td>4</td></tr>
    <tr><td>l</td><td>long</td><td>integer</td><td>4</td></tr>
    <tr><td>L</td><td>unsigned long</td><td>integer</td><td>4</td></tr>
    <tr><td>q</td><td>long long</td><td>integer</td><td>8</td></tr>
    <tr><td>Q</td><td>unsigned long long</td><td>integer</td><td>8</td></tr>
    <tr><td>n</td><td>ssize_t</td><td>integer</td><td></td></tr>
    <tr><td>N</td><td>size_t</td><td>integer</td><td></td></tr>
    <tr><td>f</td><td>float</td><td>float</td><td>4</td></tr>
    <tr><td>d</td><td>double</td><td>float</td><td>8</td></tr>
    <tr><td>s</td><td>char[]</td><td>bytes</td><td></td></tr>
    <tr><td>p</td><td>char[]</td><td>bytes</td><td></td></tr>
    <tr><td>P</td><td>void *</td><td>integer</td><td></td></tr>
</table>

It’s straightforward enough that a couple of examples will suffice.

---

##### burnTx

    READWRITE(burnCTx); // s32int

The Slimcoin-specific `s32int` is an “int” according to `util.h` (i.e. an  integer). An integer in the Python struct map occupies 4 bytes, so we need to read 4 bytes of the block in order to consume the data encoded for `burnTx`.

---

##### hashBurnBlock

     READWRITE(hashBurnBlock); // uint256

`uint256` has its own [C++ definitional header file](https://github.com/slimcoin-project/Slimcoin/blob/slimcoin/src/uint256.h) but fortunately, we’re spared the full C++ gory details of stonking big 256-bit/32-byte unsigned integers because we see them as block and transaction hashes so we can just vacuum up 32 sequential bytes to read in the data:

    hashburnblock = ds.read_bytes(32)[::-1].hex()


---

What’s the `[::-1]` for? It’s the Python syntax for reversing a sequence.

It’s used because the data is stored as little-endian (check the raw dump above). My Linux laptop is big-endian which means that any *sequence* of bytes read off the blockchain appears reversed.

Thus, reading the 4 bytes for `nBits` will result in the little-endian `ffff0f1e` instead of the (correct) big-endian `1e0fffff`. Reversing the sequence of bytes restores the correct semantics.

### Doing for ourselves

So, working from the assembled information, we can adapt the snippet of the Python pattern reader code that we used earlier to guide us on identifying the pattern and extend it to read the Slimcoin-specific data encoded in the block.

I have taken advantage of some other, datatype-specific routines that are handily available in order to make the additions a little more self-explanatory as to what they are intended to do ...

```python
# Read file
# https://bitcoin.org/en/developer-reference#block-headers
# https://en.bitcoin.it/wiki/Protocol_specification#block
magic = ds.read_bytes(4).hex()
block_size = int(struct.pack('>l', *struct.unpack('<l', ds.read_bytes(4))).hex(), 16)
version = struct.pack('>l', *struct.unpack('<l', ds.read_bytes(4))).hex()
prev_header_hash = ds.read_bytes(32)[::-1].hex()
merkle_root_hash = ds.read_bytes(32)[::-1].hex()
timestamp = ds.read_bytes(4)[::-1].hex()
nBits = ds.read_bytes(4)[::-1].hex()
nonce = ds.read_bytes(4)[::-1].hex()

fproofofburn = ds.read_boolean()
hashburnblock = ds.read_bytes(32)[::-1].hex()
burnhash = ds.read_bytes(32)[::-1].hex()
burnblockheight = ds.read_int32()
burnctx = ds.read_int32()
burnctxout = ds.read_int32()
neffectiveburncoins = ds.read_int64()
nburnbits = ds.read_uint32()

num_of_transaction = ds.read_bytes(1)[::-1].hex()
tx_version = ds.read_bytes(4)[::-1].hex()
tx_ntime = ds.read_bytes(4)[::-1].hex()
tx_input = ds.read_bytes(1)[::-1].hex()
tx_prev_output_hash = ds.read_bytes(32)[::-1].hex()
tx_prev_output_sequence = ds.read_bytes(4)[::-1].hex()
coinbase_tx_length = ds.read_bytes(1)[::-1].hex()
coinbase_tx = ds.read_bytes(int((coinbase_tx_length), 16)).hex()
sequence = ds.read_bytes(4)[::-1].hex()
tx_output = ds.read_bytes(2)[::-1].hex()
BTC_num = ds.read_bytes(8)[::-1].hex()
pk_script_len = ds.read_bytes(1)[::-1].hex()
pk_script = ds.read_bytes(int(pk_script_len, 16))[::-1].hex()
lock_time = ds.read_bytes(4)[::-1].hex()
```

You may have noticed that at the beginning of the block there a couple of data fields `magic` and `block_size` that don’t appear in the block C++ READ/WRITE structure.

They are meta-data and are used to mark the start and end (start + `block_length`) of each block.

By convention, each coin *should* have its own (misleadingly-named) [`pchMessageStart`](https://github.com/slimcoin-project/Slimcoin/blob/slimcoin/src/protocol.cpp#L25) (aka “magic bytes”), a unique 4-byte sequence of “unlikely” values to use to mark the start of each block in its blockchain. 

Slimcoin’s [4 “magic bytes”](https://github.com/slimcoin-project/Slimcoin/blob/slimcoin/src/protocol.cpp#L25) `6e8b92a5` are indeed unique amongst altcoins (AFAIK):

    static unsigned char pchMessageStartSLIMCoin[4] = { 0x6e, 0x8b, 0x92, 0xa5 };

The algorithm for reading a block is:

> find and consume the 4 Slimcoin magic bytes, then read 4 more little-endian bytes into `block_size` and intepret them as an integer specifying the length of the block in bytes then consume `block_size` more bytes.

We **know** what we are *supposed* to get ...

```c++
// Genesis block
const char *pszTimestamp = "RT: 2 southeast Ukranian regions to hold referendum \
May 11 as planned";
CTransaction txNew;
txNew.nTime = !fTestNet ? 1399578460 : 1390500425;
txNew.vin.resize(1);
txNew.vout.resize(1);
txNew.vin[0].scriptSig = CScript() << 486604799 << CBigNum(9999) \
    << vector<unsigned char>(
        (const unsigned char*)pszTimestamp,
        (const unsigned char*)pszTimestamp + strlen(pszTimestamp));
txNew.vout[0].SetEmpty();
CBlock block;
block.vtx.push_back(txNew);
block.hashPrevBlock = 0;
block.hashMerkleRoot = block.BuildMerkleTree();
block.nVersion = 1;
block.nTime    = !fTestNet ? 1399578460 : 1390500425;
block.nBits    = bnProofOfWorkLimit.GetCompact();
block.nNonce   = !fTestNet ? 116872 : 63626;
```

> As with all poetry, most people can read program code but not write it - so a few curly brackets and semicolons shouldn’t necessarily spoil your day.

In the above - the `pszTimestamp` is bound to a string that, by convention, uses a media headline to nail the date that the genesis block was created and acts an informal (read ineffectual) “proof” that there was no previous mining.

Then the genesis transaction `txNew` is instantiated, its `nTime` bound to 1399578460 if we’re on mainnet.

The transaction data-carrying substructures `vin` and `vout` are initialised and a `CScript` (constructed from the arguments given, including the `pszTimestamp`) is written to the `scriptSig` field of `vin`. `vout` is marked as empty.

A new block `block` is instantiated and `txNew` is pushed into the `vtx` vector used for collecting up transactions. The rest of the block fields are bound according to either explicit declaration or computed values that we already know from inspecting the output of `getblock`.

### The Anatomy


    6e 8b 92 a5 // magic: (0x6e8b92a5) (4 verbatim bytes)
    39 01 00 00 // block_size: 313 (0x00000139) (4 * 1 byte (00-ff each), reversed)
    01 00 00 00 // version: 00000001 (4 * 1 byte (00-ff each), reversed)
    0000000000000000000000000000000000000000000000000000000000000000 // hashPrevBlock (reversed)
    bae3867d5e5d35c321adaf9610b9e4147a855f9ad319fdcf70913083d783753f // hashMerkleRoot (reversed)
    5c df 6b 53 // nTime: 2014-05-08T20:47:40 (4 * 1 byte (00-ff each), reversed) 
                // datetime.fromtimestamp(0x536bdf5c).isoformat()
    ff ff 0f 1e // nBits: 1e0fffff (4 * 1 byte (00-ff each), reversed)
    88 c8 01 00 // nNonce: 116872 (0x0001c888) (4 * 1 byte (00-ff each), reversed)
    00 // proof-of-burn (1 byte boolean)
    0000000000000000000000000000000000000000000000000000000000000000 // hashburnblock (reversed)
    0000000000000000000000000000000000000000000000000000000000000000 // burnhash (reversed)
    ff ff ff ff // burnblockheight: (4 * 1 byte (00-ff each), reversed) 
    ff ff ff ff // burnctx: (4 * 1 byte (00-ff each), reversed)
    ff ff ff ff // burnctxout: (4 * 1 byte (00-ff each), reversed)
    00 00 00 00 // neffectiveburncoins: (4 * 1 byte (00-ff each), reversed)
    00 00 00 00 // nburnbits: (4 * 1 byte (00-ff each), reversed)
    00 // num_of_transaction: 0 (1 byte)
    00 00 00 01 // tx_version: 
    01 00 00 00 // tx_version: 1 (0x000001) (4 * 1 byte (00-ff each), reversed)
    5c df 6b 53 // tx_ntime: 2014-05-08T20:47:40 (4 * 1 byte (00-ff each), reversed) 
                // datetime.fromtimestamp(0x536bdf5c).isoformat()
    01 // input: 1 (1 byte)
    0000000000000000000000000000000000000000000000000000000000000000 // prev_output_hash (reversed)
    ff ff ff ff // prev_output_num: (0xffffff) (4 * 1 byte (00-ff each), reversed)
    4e // script_length: 78 (0x4e)
    04ffff001d020f274552543a203220736f7574686561737420556b72616e69616e207265676
    96f6e7320746f20686f6c64207265666572656e64756d204d617920313120617320706c616e
    6e6564 // scriptsig (script_length (78 verbatim bytes)
    ff ff ff ff // sequence
    01 00 00 00 // tx_version: 1 (0x000001) (4 * 1 byte (00-ff each), reversed)
    00 // tx_output_num: 0
    00 00 00 00 00 00 00 00 // BTCnum:  (8 * 1 byte (00-ff each), reversed)
    00 // pk_script_len: 0 
    00 // pk_script: zero
    00 00 00 00 00 00 00 00 // lock_time

### Follow-up

With a couple of trivial fixes, the Python code posted to Bitcoin Stackexchange can be adapted to run under Python 3:

```python
import struct  # conversion between Python values and C structs as Python strings
try:
    import StringIO  # Reads and writes a string buffer
except ImportError:
    from io import StringIO
import os
import mmap  # mutable string
from binascii import unhexlify, hexlify

class BCDataStream(object):
    def __init__(self):
        self.input = None
        self.read_cursor = 0

    def clear(self):
        self.input = None
        self.read_cursor = 0

    def write(self, bytes):  # Initialize with string of bytes
        if self.input is None:
            self.input = bytes
        else:
            self.input += bytes

    def map_file(self, file, start):  # Initialize with bytes from file
        self.input = mmap.mmap(file.fileno(), 0, access=mmap.ACCESS_READ)
        self.read_cursor = start

    def seek_file(self, position):
        self.read_cursor = position

    def close_file(self):
        self.input.close()

    def read_string(self):
        # Strings are encoded depending on length:
        # 0 to 252 :  1-byte-length followed by bytes (if any)
        # 253 to 65,535 : byte'253' 2-byte-length followed by bytes
        # 65,536 to 4,294,967,295 : byte '254' 4-byte-length followed by bytes
        # ... and the Bitcoin client is coded to understand:
        # greater than 4,294,967,295 : byte '255' 8-byte-length followed by bytes of string
        # ... but I don't think it actually handles any strings that big.
        if self.input is None:
            raise SerializationError("call write(bytes) before trying to deserialize")

        try:
            length = self.read_compact_size()
        except IndexError:
            raise SerializationError("attempt to read past end of buffer")

        return self.read_bytes(length)

    def write_string(self, string):
        # Length-encoded as with read-string
        self.write_compact_size(len(string))
        self.write(string)

    def read_bytes(self, length):
        try:
            result = self.input[self.read_cursor:self.read_cursor + length]
            self.read_cursor += length
            return result
        except IndexError:
            raise SerializationError("attempt to read past end of buffer")

        return ''

    def read_boolean(self):
        return self.read_bytes(1)[0] != chr(0)

    def read_int16(self):
        return self._read_num('>h')

    def read_uint16(self):
        return self._read_num('>H')

    def read_int32(self):
        return self._read_num('>i')

    def read_uint32(self):
        return self._read_num('>I')

    def read_int64(self):
        return self._read_num('>q')

    def read_uint64(self):
        return self._read_num('>Q')

    def write_boolean(self, val):
        return self.write(chr(1) if val else chr(0))

    def write_int16(self, val):
        return self._write_num('>h', val)

    def write_uint16(self, val):
        return self._write_num('>H', val)

    def write_int32(self, val):
        return self._write_num('>i', val)

    def write_uint32(self, val):
        return self._write_num('>I', val)

    def write_int64(self, val):
        return self._write_num('>q', val)

    def write_uint64(self, val):
        return self._write_num('>Q', val)

    def read_compact_size(self):
        size = ord(self.input[self.read_cursor])
        self.read_cursor += 1
        if size == 253:
            size = self._read_num('>H')
        elif size == 254:
            size = self._read_num('>I')
        elif size == 255:
            size = self._read_num('>Q')
        return size

    def write_compact_size(self, size):
        if size < 0:
            raise SerializationError("attempt to write size < 0")
        elif size < 253:
            self.write(chr(size))
        elif size < 2**16:
            self.write('\xfd')
            self._write_num('>H', size)
        elif size < 2**32:
            self.write('\xfe')
            self._write_num('>I', size)
        elif size < 2**64:
            self.write('\xff')
            self._write_num('>Q', size)

    def _read_num(self, format):
        (i,) = struct.unpack_from(format, self.input, self.read_cursor)
        self.read_cursor += struct.calcsize(format)
        return i

    def _write_num(self, format, num):
        s = struct.pack(format, num)
        self.write(s)

def import_blkdat():
        pass

ds = BCDataStream()
with open("/home/{}/.slimcoin/blk0001.dat".format(os.environ['USER']), "rb") as file:
    ds.map_file(file, 0)

# Read file
    # https://bitcoin.org/en/developer-reference#block-headers
    # https://en.bitcoin.it/wiki/Protocol_specification#block
    magic = ds.read_bytes(4).hex()
    block_size = int(struct.pack('>l', *struct.unpack('<l', ds.read_bytes(4))).hex(), 16)
    version = struct.pack('>l', *struct.unpack('<l', ds.read_bytes(4))).hex()
    prev_header_hash = ds.read_bytes(32)[::-1].hex()
    merkle_root_hash = ds.read_bytes(32)[::-1].hex()
    timestamp = ds.read_bytes(4)[::-1].hex()
    nBits = ds.read_bytes(4)[::-1].hex()
    nonce = ds.read_bytes(4)[::-1].hex()

    fproofofburn = ds.read_boolean()
    hashburnblock = ds.read_bytes(32)[::-1].hex()
    burnhash = ds.read_bytes(32)[::-1].hex()
    burnblockheight = ds.read_int32()
    burnctx = ds.read_int32()
    burnctxout = ds.read_int32()
    neffectiveburncoins = ds.read_int64()
    nburnbits = ds.read_uint32()

    num_of_transaction = ds.read_bytes(1)[::-1].hex()
    tx_version = ds.read_bytes(4)[::-1].hex()
    tx_ntime = ds.read_bytes(4)[::-1].hex()
    tx_input = ds.read_bytes(1)[::-1].hex()
    tx_prev_output_hash = ds.read_bytes(32)[::-1].hex()
    tx_prev_output_sequence = ds.read_bytes(4)[::-1].hex()
    coinbase_tx_length = ds.read_bytes(1)[::-1].hex()
    coinbase_tx = ds.read_bytes(int((coinbase_tx_length), 16)).hex()
    sequence = ds.read_bytes(4)[::-1].hex()
    tx_output = ds.read_bytes(2)[::-1].hex()
    BTC_num = ds.read_bytes(8)[::-1].hex()
    pk_script_len = ds.read_bytes(1)[::-1].hex()
    pk_script = ds.read_bytes(int(pk_script_len, 16))[::-1].hex()
    lock_time = ds.read_bytes(4)[::-1].hex()
    # If all the data in the genesis block has been read, then the next
    # four bytes should be the "magic bytes" denoting the start of the
    # next block
    nextmagic = ds.read_bytes(4).hex()

    print('magic: {} (6e, 8b, 92, a5)'.format(magic))
    print('block_size: {}'.format(block_size))
    print('version: {}'.format(version))
    print('prevhash: {}'.format(prev_header_hash))
    print('merkle_root: {}'.format(merkle_root_hash))
    print('timestamp: {})'.format(
        int(timestamp, 16), datetime.fromtimestamp(int(timestamp, 16)).isoformat()))
    print('nBits: {}'.format(nBits))
    print('nonce: {}'.format(int(nonce, 16)))

    print('fproofofburn: {}'.format(fproofofburn))
    print('hashburnblock: {}'.format(hashburnblock))
    print('burnhash: {}'.format(burnhash))
    print('burnblockheight: {}'.format(burnblockheight))
    print('burnctx: {}'.format(burnctx))
    print('burnctxout: {}'.format(burnctxout))
    print('neffectiveburncoins: {}'.format(neffectiveburncoins))
    print('nburnbits: {}'.format(nburnbits))

    print('--------------------- Transaction Details: ---------------------')
    print('num_of_transaction: {}'.format(int(num_of_transaction, 16)))
    print('tx_version: {}'.format(tx_version))
    print('tx_ntime: {} ({})'.format(tx_ntime, datetime.fromtimestamp(int(tx_ntime, 16)).isoformat()))
    print('tx_input_num: {}'.format(int(tx_input, 16)))
    print('tx_prev_output_hash: {}'.format(tx_prev_output_hash))
    print('tx_prev_output_sequence: {}'.format(tx_prev_output_sequence))
    print('coinbase_tx_length: {}'.format(coinbase_tx_length))
    print('coinbase_tx: {}'.format(coinbase_tx))
    print('sequence: {}'.format(sequence))
    print('tx_output_num: {}'.format(tx_output))
    print('BTC_num: {}'.format(BTC_num))
    print('pk_script_len: {}'.format(pk_script_len))
    print('pk_script: {}'.format(pk_script))
    print('lock_time: {} ({})'.format(lock_time, datetime.fromtimestamp(int(lock_time, 16)).isoformat()))
    print('----------------------- End of Block: ------------------------')
    print('nextmagic: {} (6e, 8b, 92, a5)'.format(nextmagic))

ds.close_file()

```
    magic: 6e8b92a5 (6e, 8b, 92, a5)
    block_size: 313
    version: 00000001
    prevhash: 0000000000000000000000000000000000000000000000000000000000000000
    merkle_root: bae3867d5e5d35c321adaf9610b9e4147a855f9ad319fdcf70913083d783753f
    timestamp: 1399578460 (2014-05-08T20:47:40)
    nBits: 1e0fffff
    nonce: 116872
    fproofofburn: True
    hashburnblock: 0000000000000000000000000000000000000000000000000000000000000000
    burnhash: 0000000000000000000000000000000000000000000000000000000000000000
    burnblockheight: -1
    burnctx: -1
    burnctxout: -1
    neffectiveburncoins: 0
    nburnbits: 0
    --------------------- Transaction Details: ---------------------
    num_of_transaction: 1
    tx_version: 00000001
    tx_ntime: 536bdf5c (2014-05-08T20:47:40)
    tx_input_num: 1
    tx_prev_output_hash: 0000000000000000000000000000000000000000000000000000000000000000
    tx_prev_output_sequence: ffffffff
    coinbase_tx_length: 4e
    coinbase_tx: 04ffff001d020f274552543a203220736f7574686561737420556b72616e69616e20726567696f6e73\
                 20746f20686f6c64207265666572656e64756d204d617920313120617320706c616e6e6564
    sequence: ffffffff
    tx_output_num: 0001
    BTC_num: 0000000000000000
    pk_script_len: 00
    pk_script: 
    lock_time: 00000000 (1970-01-01T01:00:00)
    ----------------------- End of Block: ------------------------
    nextmagic: 6e8b92a5 (6e, 8b, 92, a5)

`pk script`, being of length zero, results in zero bytes being read, allowing the remaining bytes to be read into `lock_time`, bringing us to the end of the Slimcoin genesis block.

End of writeup

---

