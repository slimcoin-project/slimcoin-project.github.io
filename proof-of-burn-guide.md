---
title: Poradnik wydobycia metodą Proof of Burn
lang: pl
category: help
ref: pobguide
layout: page
permalink: /proof-of-burn-guide/
---

**Burning** is the distinctive feature of Slimcoin. Here you find a guide how to earn Slimcoins by burning.

**Niszczenie** jest główną innowacyjną funkcją Slimcoin'a. Tutaj dowiesz jak zdobywać Slimcoin'y, przez niszczenie.

### How it works

You destroy a part of your coins sending them to an unspendable address, the **burn address**, using a special command. When the system detects that you burnt coins, your address gets a **score** called **Effective Burnt Coins** that determines your chance to find blocks. This score is higher if you burnt more coins.

Don't be afraid to burn too few coins - you can always rise your score burning more coins from the same address.

While burning, you not only can get rewards but also help regulating the money supply. [Learn more about Proof of Burn](/proof-of-burn-eli5/) in our simple explanation.

**Note**: The *Effective Burnt Coins* score decreases ("decays") a little bit every block to avoid attacks by early adopters and to mimic the aging of mining equipment, but the score is positive for over one year for every coin you burnt. So you have plenty of time to benefit from your burnt coins.

### Jak to działa

Niszczysz część swoich monet wysyłając je do adresu, z którego nie da się ich wydać, tzw. **burn address**, używając specjalnej komendy. Jeśli system wykryje, że zniszczyłeś monety, Twój adres dostaję **wynik** zwany **Efektywnym zniszczeniem monet** który warunkuję Twoje szanse do znajdowania bloków. Wynik ten jest tym wyższy im więcej zniszczysz monet.

Nie bój niszczyć za mało monet - możesz zawsze podwyższyć **wynik**, niszcząc więcej monet z tego samego adresu.

Podczas niszczenia, możesz nie tylko dostawać nagrody, lecz też pomagasz w regulowaniu podaży pieniądza [Sprawdź więcej co to Proof of Burn](/proof-of-burn-eli5/) w naszym wyjaśnieniach.

**Note**: *Efektywne zniszczone monety* wynik zmniejsza się ("wygasa") trochę przy każdym blocku, aby uniknąć ataku przez wczesnych użytkowników i aby imitować starzenie się sprzętu do kopania, ale wynik jest pozytywny po ponad roku roku dla każdej monety, którą zniszczysz. Masz więc sporo czasu, aby czerpać pożytek z Twoich zniszczonych monet. 

### Requirements

You need a Slimcoin client (graphical client or daemon) and some Slimcoins. That's all! No mining equipment or other hardware is required.

To have chances to find blocks regularly, you should burn at least 100, or better 1000 Slimcoins.

**Important**: If you wallet is encrypted, you must unlock it to be able to mint. In the graphical client, you should use the following command in the console (*Help* -> *Debug window* -> *Console* tab):

```walletpassphrase PASSPHRASE TIME```

In the daemon, you unlock it with the following RPC command:

```slimcoind walletpassphrase PASSPHRASE TIME```

PASSPHRASE being your passphrase and TIME the time it should be unlocked (in seconds). If you want to unlock it indeterminately simply choose a large number, e.g. 999999999.

### Wymagania

Potrzebujesz klienta Slimcoin'a (graficznego bądź daemon'a), i trochę Slimcoin'ów. To wszystko. Nie potrzebujesz sprzętu do kopania, czy innego sprzętu.

Aby mieć szansze znajdownania bloków regularnie, powinnieneś zniszczyć conajmniej 100, a najlepiej 1000 Slimcoin'ów.

**Ważne**: Jeśli Twój portfel jest zaszyfrowany, musisz go odblokować najpierw przed zaczęciem wydobywania. W graficznym kliencie, powinneś użyc podanych komend w konsoli (*Help* -> *Debug window* -> *Console* karta/zakładka):

```walletpassphrase PASSPHRASE TIME```

W daemonie, aby odblokować go użyj danej komendy RPC:

```slimcoind walletpassphrase PASSPHRASE TIME```

PASSPHRASE jest twoim hasłem, a TIME oznacza czas na jaki chcesz go odblokować (w sekundach). Jeśli chcesz odblokować na bardzo długi czas, po prostu wybierz dużą liczbę, np. 9999999999.

### Burning with the graphical client

In the graphical client, a graphical item called **Burn Coins** is provided which makes it very easy to burn coins. It is accessible from the main window or via the **Tools** menu.

Simply **enter the amount** you want to burn in the window that appears and click OK. Wait until the burnt coint have matured and then you will receive rewards every time you find a block.

**Note**. Burning normally costs a transaction fee of 0.01 Slimcoins per kilobyte, like all transactions. Sometimes, if the transaction is very large because you use many inputs, the client will tell you that he will add a higher fee for this transaction.

### Niszczenie z graficznym klientem

W graficznym kliencie, znajduję się przycisk **Burn Coins** który powoduję, że bardzo łatwo zniszczyć monety. Jest możliwy do zlokowalizowania z głownego okna albo z **Tools** menu.

### Burning with the daemon

With the daemon it's also very easy to burn.

Simply type the following command in the terminal:

```slimcoind burncoins AMOUNT```

being AMOUNT the amount in entire Slimcoins. (You also can use this command in the Debug console in the graphical client).

### Niszczenie z daemonem 

Z daemonem również łatwo niszczyć.

Po prostu wpisz tą komendę w terminalu:

```slimcoind burncoins AMOUNT```

AMOUNT oznacza ilość Slimcoin'ów do zniszczenia.


### Get information about burning

With the following command you get some basic information about the state of the Proof of Burn system:

```slimcoind getburndata```

You get the following indicators:

* **Net Burnt Coins** is the total amount of coins you have burnt.
* **Effective Burnt Coins** is your score: it is the number of coins you burnt minus the decayed burnt coins.
* **Inmature Burnt Coins** are coins you burnt but still haven't matured. The maturing period is XX blocks.
* **Decayed Burnt Coins** is the amount of coins being deducted from your score (see above) to avoid early adopter attacks and make burning fairer.

* **Formatted nEffectiveBurnCoins** is the sum of the "Effective Burnt Coins" score of all acounts together. It is a rough measure to calculate the amount of coins you have to burn if you want to find blocks regularly: the higher this value, the higher the amount of coins you should burn.
* **nEffectiveBurnCoins** is another way to display the Effective Burnt coins score.
* **nBurnBits** is a technical term referring to the *burn hash target* stored in the current block (for details, see the Whitepaper).
* **General info** is probably not being used actually.

### Więcej informacji o niszczenia

Z podaną komendą dostaniesz, podstawowe informacje o stanie systemu Proof of Burn:

```slimcoind getburndata```

Dostaniesz podane wskaźniki:

* **Net Burnt Coins** czyli całkowita ilość monet, które zniszczyłeś.
* **Effective Burnt Coins** jest twoim wynikiem: jest to liczba monet, które zniszczyłeś minus przeterminowane zniszczone monety.
* **Inmature Burnt Coins** są to monety, które zniszczyłeś, ale jeszcze nie "dojrzały" (zapadalność - jak obligacje skarbowe)
* **Decayed Burnt Coins** jest to liczość monet, które są odejmowane od Twojego wyniku (zobacz powyżej), aby uniknąć atak wczesnych użytkowników, i zrobić proces niszczenia sprawiedliwym

* **Formatted nEffectiveBurnCoins** jest sumą "Efektywnych zniszczonych monet", które zsumują się razem. Jest to surowa miara do skalkulowania ilości monet, które musisz zniszczyć, jeśli chcesz, aby znajdować bloki regularnie: im wyższa jest ta wartośc, tym większa wymagana ilość monet, którą powinnieneś zniszczyć, by otrzymać nagrodę.
* **nEffectiveBurnCoins** jest innym sposobem, aby wyświetlić, Efektywny wynik niszczenia monet
* **nBurnBits** jest technicznym terminem, który odnosi się do *niszczenia celu hash *, który jest przechowywana w obecnym bloku (więcej detali, znajdziesz w Whitepaper)
* **General info** prawdopodobnie nie używane

### How many coins have been burnt until today?

You could think the *Formatted nEffectiveBurnCoins* number is what you need, but it is not - because this number does not contain the *Decayed Burnt Coins* and is probably much smaller.

To see the real number you must check the **burn address**. In the built-in block explorer of the client or any other block explorer (e.g. [Slimcoin.club](http://www.slimcoin.club/#blkexp), enter the following address:

**SfSLMCoinMainNetworkBurnAddr1DeTK5**

In June 2017, the address had roughly a balance of 1,931 million Slimcoins; at that time that were about 12% of the total supply of 16 million.

### Jaką ilość monet została zniszczona do dzisiaj

Możesz myśleć, że wystarcza liczba *Formatted nEffectiveBurnCoins* jest wszystkim co potrzebne, ale niestety nie - ponieważ ta liczba nie zawiera, tzw. *przeterminowanych zniszczonych monet* i jest proawdpodobnie dużo mniejsza

Aby zobaczyć realną liczbą musisz sprawdzić tzw. **adres zniszczonych monet**. We wbudowanym block explorze klienta Slimcoin'a, bądź innym block explorerze, np. ([Slimcoin.club](http://www.slimcoin.club/#blkexp), i wpisać adres:

**SfSLMCoinMainNetworkBurnAddr1DeTK5**

W czerwcu 2017, adres posiadał ok. 1.931 miliona Slimcoin'ów; w tym czasie było to ok. 12% całej podaży z 16 milionów.
