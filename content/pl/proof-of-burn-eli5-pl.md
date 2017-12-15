---
title: Co to jest Proof of Burn (ELI5)?
lang: pl
menuitem: Proof of Burn ELI5
category: technology
ref: eli5
layout: page
permalink: /proof-of-burn-eli5-pl/
priority: 4
---

W tym artykule, wyjaśnimy co to jest rewolucyjny mechanizm konsensusu kryjący się w Slimcoin'ie: **Proof of burn**.

*Jeśli potrzebujesz, szybkie streszczenia, znajduję się ono **[tl;dr](#tldr)** na końcu sekcji. Czytelnicy zaznajomieni z Bitcoin'em i konsensusem Proof of Work i **dlaczego** to działa, mogą pominać pierwsze dwie sekcję.*

### Dlaczego konsensus jest potrzebny?

Aby zrozumieć co to jest Proof of Burn, po pierwsze musimy zrozumieć, dlaczego kryptowaluty używają tzw. "metody konsensusu"/

Po pierwsze, podstawy: blockchain (rozproszony rejestr publiczny) jest **główną bazą danych** kryptowaluty. Posiada wszystkie poprawnie zawarte transakcję.

Wszystkie węzły - wszyscy uczestnicy, którzy mają uruchomiony w pełni funkcjonalny klient oprogramowania - zapisują blockchain (rozproszony rejestr publiczny), na swoich dyskach twardych. Jest on nazywany blockchain'em, gdyż tranzakcje są grupowane w **blocki**. Block jest zapisywany, gdy wszystkie węzły, się zgodzą, że dane transakcje, postrzegają jako są prawidłowe.

Ale **jak węzły zgadzają się**, które transakcje powinny być zapisane w bloku? Nie ma centralnego ośrodka władzy, który potwierdza transkacje, więc tą pracę muszą wykonywać węzły, współpracując.

Technologia blockchain, już zapobiega, aby niektóre węzły nie mogły tworzyć pieniędzy z powietrza. Ale nadal mogą byc nieuczciwe pewne węzły, które będą próbować użyc danych monet drugi raz - tzw. **podwójne wydanie/zapłata**, Na przykład, mogą kupić przedmiot w sklepie internetowym i natychmiast spróbować wysłać te same monety na giełdę. W ten sposób mogą zmylić właścieciela sklepu i giełdy, i dostać obie rzeczy - przedmioty i pieniądze.

Jak *zapobiegać podwójnemu wydawaniu*, węzły muszą **przejść do porozumienia** które transakcje są prawidłowe, a które nie są.

### Proof of work: mechanizm konsensusu Bitcoin'a

Więc potrzebujemy mechanizmu głosowania, który nie da się zmanipulować, tworząc więcej węzłów.

W Bitcoin'ie, i wielu innych kryptowalutach, mechanizm, który nazywa się **Proof of work** jest używany.

Możemy go opisać jako proces: węzły (*górnicy*), rywalizują, aby zapisać blok w blockchain'ie. Aby uwzględnić blok, ich komputery muszą najpierw wykonać jakąś *pracę*: muszą **rozwiązać wymagające kryptograficzne puzzle**. Węzeł, który pierwszy rozwiąże, dostaję prawo, aby zapisać blok, i nagrodę w zamian za tą pracę. Ten proces nazywa się kolokwialnie, **kopaniem**.

Jeśli chcesz **podwójnie wydać**, musisz mieć moc obliczeniową, aby **zapisać wiele bloków w ciągu**. Tylko w ten sposób, jesteś w stanie być pewny, że obie transakcje są uwzględnione w blockchaini'e.

Aby stało się to możliwe musisz mieć **dużo mocy obliczeniowej** - możesz być tylko pewny, by zapisać wiele bloków na raz, tylko wtedy, jeśli masz więcej niż połowa, całej mocy obliczeniowej wszystkich węzłów sieci (tzw. **atak 51%**). Atak podwójnego wydania jest zapobiegany, ponieważ jest to bardzo kosztowne, aby kupić tyle mocy obliczeniowej, aby to zrealizować.

### Proof of burn: Proof of work, bez zużywania energii

Ważną rzeczą jest, aby zrozumieć, jest, że czysta moc obliczeniowa nie jest istotna, aby zapobiegać manipulacjom, podwójnego wydawania. Co jest ważne to **koszt** mocy obliczeniowej. **Musi to być kosztowne** dla atakującego, aby uzyskał taką moc, by *kopać* wiele bloków na raz.

Więc w Proof of work, prawo do kopania bloków jest powiązane z kosztem monetarnym górnika. **Im więcej górnik zapłaci** za sprzęt komputerowy, który umożliwa rozwiązywanie zagadek kryptograficznych (*koparki*), **tym więcej ma szans** aby uzyskać prawo do wykopania bloku.

Ale co jeśli możemy uzyskać ten same efekt w bardziej bezpośredni sposób?

Możemy imitować, ten koszt, dając węzłom "niszczyć" monety, jeśli chcą mieć prawo do zapisania bloku. **Jest to  reguła, za którą stoi Proof of Burn**. Nazywamy to **wytwarzaniem**, ponieważ żadna realna praca nie jest wytwarzana. Zapamiętaj: wszystko co jest najważniejsze, jest koszt mechanizmu.

To brzmi szalenie. Ale genialny umysł, który wymyślił Proof of Burn, Iain Stewart, porównował to z analogią: **Zniszczone monety są koparkami**.

To oznacza: proces *niszczenia monet* może być porównany do procesu *kupowania koparek, bądź mocy obliczeniowej*. W Proof of Burn, za każdym razem gdy, zniszczysz monety **kupujesz wirtualną koparkę**, która daję Ci moc do kopania bloków. **Im więcej monet zniszczysz, tym więcej będziesz posiadał wirtualnych koparek**.

Na tym dokładnie polega Slimcoin'a tzw. Proof of Burn mechanizm wytwarzania monet:

Jeśli niszczysz monety, **nie dostajesz tylko** prawa do rywalizowania o następny blok. Koparka jest czymś bardziej wytrzymałym, **i takie są Slimcoin'a wirtualne koparki**. Niszczysz monety, a to zwiększa Twoje szanse na dostanie większej ilości bloków przez długi okres - **co najmniej przez rok**.

Teraz, **aby wcześni uczestnicy nie mieli dużej przewagi**, albo by nie zaatakowali systemu, moc zniszczonych monet **zanika** za każdym razem, gdy blok jest wykopywany. Nie zanika mocno, więc nie bój się - będziesz mieć mnóstwo czasu. Ale imituję to kopanie: koparki stają się w końcu **przestarzałe**, ponieważ jest już lepsza technologia dostępna. Więc górnicy, aby pozostać konkurencyjnym, będą musieli wymienić, swój sprzęt od czasu do czasu. Taka sama idea stoi za Proof of Burn: jeśli chcesz utrzymać swoją moc wytwarzania monet, musisz niszczyć monety cyklicznie.

Podobnie jak w Proof of Work, **nagrody z bloków są dość wysokie**, aby umożliwić uczestnikom, mieć finansowe korzyści, z wytwarzania. Nie zwróci się Twoja inwestycja w ciągu kilku godzin, czy dni, lecz z dozą cierpliwości, w praktyce dostaniesz **znacznie więcej monet niż zniszczyłeś**.

Proof of Burn ma główną zaletę nad Proof of Work, którą jest mocne zmniejszenie zużycia energii. Więc Slimcoin jest wyborem, jeśli się martwiłeś o Bitcoin'a koszt dla środowiska. Ale Proof of Burn, ma także zalety nad Proof of Stake, innym konsensusem, który minimalizuje energię. Poświecimy temu uwagę w następnym artykule.

### tldr

**Proof of Burn działa jak wirtualne koparki: kupujesz wirtualną koparkę, jeśli zniszczysz monety. Im więcej monet zniszczysz, tym posiadasz więcej wirtualnych koparek. Każda koparka daję Ci prawo do kopania przez długi czas, tak jak w przypadku realnej koparki. Ale w końcu straci swoją moc - tak jak realne koparki, które stają się przestarzałe, przez prawo Moore'a**
