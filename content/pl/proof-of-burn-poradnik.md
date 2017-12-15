---
title: Poradnik wydobycia metodą Proof of Burn
menuitem: Poradnik Proof of Burn
lang: pl
category: help
ref: pobguide
layout: page
permalink: /proof-of-burn-poradnik/
priority: 3
---

**Niszczenie** jest główną innowacyjną funkcją Slimcoin'a. Tutaj dowiesz jak zdobywać Slimcoin'y, przez niszczenie.

### Jak to działa

Niszczysz część swoich monet wysyłając je do adresu, z którego nie da się ich wydać, tzw. **burn address**, używając specjalnej komendy. Jeśli system wykryje, że zniszczyłeś monety, Twój adres dostaję **wynik** zwany **Efektywnym zniszczeniem monet** który warunkuję Twoje szanse do znajdowania bloków. Wynik ten jest tym wyższy im więcej zniszczysz monet.

Nie bój niszczyć za mało monet - możesz zawsze podwyższyć **wynik**, niszcząc więcej monet z tego samego adresu.

Podczas niszczenia, możesz nie tylko dostawać nagrody, lecz też pomagasz w regulowaniu podaży pieniądza [Sprawdź więcej co to Proof of Burn](/proof-of-burn-eli5/) w naszym wyjaśnieniach.

**Notka**: *Efektywne zniszczone monety* wynik zmniejsza się ("wygasa") trochę przy każdym blocku, aby uniknąć ataku przez wczesnych użytkowników i aby imitować starzenie się sprzętu do kopania, ale wynik jest pozytywny po ponad roku roku dla każdej monety, którą zniszczysz. Masz więc sporo czasu, aby czerpać pożytek z Twoich zniszczonych monet. 

### Wymagania

Potrzebujesz klienta Slimcoin'a (graficznego bądź daemon'a), i trochę Slimcoin'ów. To wszystko. Nie potrzebujesz sprzętu do kopania, czy innego sprzętu.

Aby mieć szansze znajdownania bloków regularnie, powinnieneś zniszczyć conajmniej 100, a najlepiej 1000 Slimcoin'ów.

**Ważne**: Jeśli Twój portfel jest zaszyfrowany, musisz go odblokować najpierw przed zaczęciem wydobywania. W graficznym kliencie, powinneś użyc podanych komend w konsoli (*Help* -> *Debug window* -> *Console* karta/zakładka):

```walletpassphrase PASSPHRASE TIME```

W daemonie, aby odblokować go użyj danej komendy RPC:

```slimcoind walletpassphrase PASSPHRASE TIME```

PASSPHRASE jest twoim hasłem, a TIME oznacza czas na jaki chcesz go odblokować (w sekundach). Jeśli chcesz odblokować na bardzo długi czas, po prostu wybierz dużą liczbę, np. 9999999999.

### Niszczenie z graficznym klientem

W graficznym kliencie, znajduję się przycisk **Burn Coins** który powoduję, że bardzo łatwo zniszczyć monety. Jest możliwy do zlokowalizowania z głownego okna albo z **Tools** menu.

Po prostu **wpisz ilość** jaką chcesz zniszczyć w oknie, które się pojawi i kliknij OK. Poczekaj, aż zniszczone monety dojrzeją (zapadalność jak obligacji skarbowych), i dostaniesz nagrodę za każdym razem jak znajdziesz blok (z włączonym klientem Slimcoin'a)

**Notka**. Niszczenie monet normalnie kosztuję, opłatę transakcyjną ok. 0.01 Slimcoina na kilobajt, jak inne transakcje. Czasem, jeśli transakcja, jest bardzo duża, bo masz dużo wkładu, klient Slimcoin'a doda większą opłatę transakcyjną, za tą transakcję.

### Niszczenie z daemonem 

Z daemonem również łatwo niszczyć.

Po prostu wpisz tą komendę w terminalu:

```slimcoind burncoins AMOUNT```

AMOUNT oznacza ilość Slimcoin'ów do zniszczenia.

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
* **nBurnBits** jest technicznym terminem, który odnosi się do *niszczenia celu hash*, który jest przechowywana w obecnym bloku (więcej detali, znajdziesz w Whitepaper)
* **General info** prawdopodobnie nie używane

### Jaką ilość monet została zniszczona do dzisiaj

Możesz myśleć, że wystarcza liczba *Formatted nEffectiveBurnCoins* jest wszystkim co potrzebne, ale niestety nie - ponieważ ta liczba nie zawiera, tzw. *przeterminowanych zniszczonych monet* i jest proawdpodobnie dużo mniejsza

Aby zobaczyć realną liczbą musisz sprawdzić tzw. **adres zniszczonych monet**. We wbudowanym block explorze klienta Slimcoin'a, bądź innym block explorerze, np. ([Slimcoin.club](http://www.slimcoin.club/#blkexp), i wpisać adres:

**SfSLMCoinMainNetworkBurnAddr1DeTK5**

W czerwcu 2017, adres posiadał ok. 1.931 miliona Slimcoin'ów; w tym czasie było to ok. 12% całej podaży z 16 milionów.
