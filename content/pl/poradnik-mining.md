---
title: Poradnik kopania Slimcoin'a
codeType: guide
menuitem: Poradnik kopania
lang: pl
category: help
ref: powguide
layout: page
permalink: /poradnik-mining/
priority: 2
---

### Kopanie/mining samemu

Kopanie samemu jest najłatwiejszą metodą, aby wydobywać Slimcoin. Jest to dokonywane poprzez klienta Slimcoin'a, albo oprogramowanie do kopania tzw. miner. Jeśli trudność jest niska (aktualnie jest), wtedy kopanie samemu jest zyskowne.

You can mine Slimcoin with CPUs (recommended) or with GPUs (experimental).

Możesz kopać Slimcoin z pomocą procesora (CPU), albo karty graficznej (GPU), miner GPU jest eksperymentalny i może posiadać błędy

#### Graficzny interfejs (Slimcoin-QT)

Jeśli używasz klienta graficznego, możesz kopać bezproblemu wpisując daną komendę w konsolę RPC (znajduję się w *Help* -> *Debug window* i otwórz *Console* zakładkę)

komenda to ```setgenerate true```

Możesz też wyspecjalizować ile rdzeni twojego procesora, chcesz użyć:

```setgenerate true NUMBER_OF_CORES```

NUMBER_OF_CORES oznacza ile chcesz użyć rdzeni, jeśli wszystkie chcesz użyć, wpisz:

```setgenerate true -1```

Aby skończyć kopanie, po prostu wpisz:

```setgenerate false```

Aby uzyskać informacje o kopaniu:

```getmininginfo```

**Ważne**: Z klientem Slimcoin'a - graficznym, bądź daemon, możesz tylko kopać na procesorze (CPU), a algorytm nie jest zoptymalizowany. Jeśli chcesz maksymalnej efektywności, użyć minerów do CPU, bądź GPU, które znajdują się poniżej.

#### Daemon (slimcoind)

Możesz zacząć kopanie, używając tych komend:

```slimcoind -gen```

razem z innymi opcjami, które chcesz zaaplikować.

Jeśli daemon działa, te same komendy w terminalu są obecne jak te w kliencie graficznym Slimcoin'a. Więc możesz zacząć kopanie z komendą *setgenerate true*, w konsoli debugowania.

#### Kopanie na procesorze (eksperymentalne)

Aby kopanie było optymalne, możesz użyć tzw. **Slimminer** minera. Jest to oprogramowanie eksperymentalne i możesz posiadać błędy.

Sprawdź na [Slimminer Github](https://github.com/JonnyLatte/slimminer) i podążaj za instrukcją, aby zainstalować i kopać.

#### Kopanie na karcie graficznej (eksperymentalne)

Aby moć kopać na karcie graficznej/kartach graficznych (GPUs), możesz użyć **SlimminerGPU** minera. Jest to oprogramowanie eksperymentalne i możesz posiadać błędy.
Sprawdź na [Slimminer Github](https://github.com/JonnyLatte/slimminerGPU) i podążaj za instrukcją, aby zainstalować i kopać.

### Poole

Nie ma aktualnie żadnych pooli dla Slimcoina. Lecz mamy inicjatywy, aby utworzyć pool. Więc bądźcie czujni!
