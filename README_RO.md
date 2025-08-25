# Analiza Datelor Uber

## Descriere

Acest proiect demonstrează abilitățile de analiză a datelor folosind SQL și Python. Scopul principal a fost explorarea unui set de date real, de pe platforma Kaggle, cu curse Uber și extragerea de informații relevante pentru a răspunde la întrebări de business.

## Setul de date

Setul de date a fost preluat de pe Kaggle, cu titlul "Uber Data Analytics Dashboard", și conține informații despre 150.000 de curse înregistrate.
Dataset Link:[Link to dataset from kaggle](https://www.kaggle.com/datasets/yashdevladdha/uber-ride-analytics-dashboard)

## Curățarea datelor

*  În această etapă, m-am concentrat pe pregătirea datelor pentru analiză. Am identificat un număr semnificativ de valori lipsă (NaN), utilizand functia `.isnull()` a bibliotecii Pandas, am inlocuit valorile lipsa gasite cu valori relevante, de exemplu pentru `Avg VTAT` am completat folosind mediana, cu functia `.median()`, astfel nu va influenta intr-un mod negativ viitoarele calcule statistice precum media, iar in coloanele unde valoarea lipsa este evident un `0` am completat corespunzator, spre exemplu in coloana `Cancelled Rides by Customer` este clar faptul ca unde nu exista valori, nu au existat curse anulate. Pentru coloanele text, precum `Driver Cancellation Reason` am completat valorile lipsa cu `Unkown`.
*  Am verificat daca exista randuri duplicate, mai exact daca coloana in `Booking ID` se regasesc dubluri, iar apoi le-am sters duplicatele, fiind `1233` la numar.
![Screenshot from code](/Screenshot_duplicates.png)
*  Am verificat suplimentar daca in coloanele text valorile unice sunt corespunzatoare si scrise corect cu ajutorul functiei `.unique()`. A rezultat faptul ca totul este in regula.
*  De asemenea, am luat în considerare prezența potențială a outlierilor. Am utilizat direct mediana pentru a completa valorile lipsă, o alegere strategică ce asigură că rezultatele analizei nu vor fi distorsionate de valorile extreme, deoarece mediana nu este influențată de acestea.

## Analiza și Concluzii
* In continuare vom gasi raspunsul la 5 intrebari relevante legate de randamentul dat de compania Uber, conform Table-ului primit.
### Intrebari relevante
* 1.Care sunt veniturile și a ratele de succes pe tip de vehicul?
![Screenshot from code query1](/Screenshot%20query1.png)
Dupa cum putem observa, am obtinut printr-un simplu query informatiile dorite cu privire la cele 6 vehicule de transport. Spre exemplu, pentru vehicului de tip `Premier Sedan`, am obtinut un venit total de `8599586.0` si o rata de succes a curselor de `62.161560%`. 
Aceste rezultate sunt concludente, si putem trage concluzii analizand query-ul obtinut, precum faptul ca `Auto` este tipul de vehicul cu cel mai ridicat venit total de `17711434.0`, iar categoria de vehicul `Uber XL` are cea mai mare rata de succes a curselor de `62.528268%`.

* 2.Care sunt orele de vârf și cele mai populare locații de preluare?
Am decis sa impart cele 2 intrebari in 2 query-uri diferite, `query2_hours` si `query2_Pickup_Location`.
![Screenshot from code query2](/Screenshot%20query2_hours.png)
Conform acestui query, putem observa faptul ca ora cea mai de varf este `18` cu `12298` curse totale, iar perioada cea mai aglomerata este intre 16-19, probabil datorat faptului ca undeva prin acest interval oamenii se intorc de la munca spre casa.
![Screenshot from code query2](/Screenshot%20query2_pickup_locations.png)
Query-ul cu locatiile de preluare ne ofera informatii cu privire la top 10 locuri de unde se preiau cele mai multe curse, spre exemplu cea mai frecventata locatie de preluare este `Khandsa` cu `947` de curse preluate.

* 3.Care sunt motivele de anulare a curselor și ce impact au?
![Screenshot from code query3](/Screenshot%20query3.png)
Prin acest query am grupat intr-un tabel, atat motivele de anulare ale soferilor, cat si motivele de anulare ale clientilor. Dupa cum se poate observa din rezultat, cea mai mare valoare de curse anulate au drept motiv `Unknown`, acest lucru este rezultat din faptul ca erau foarte multe valori lipsa, de tip `NaN`, iar in procesul de curatare a datelor le-am notat astfel. Acest lucru semnifica faptul ca procesul de colectare a datelor nu a fost tocmai optim efectuat sau atat clientii, cat si soferii au anulat multe curse fara a oferi un motiv concludent, iar acest lucru aduce o pierdere firmei de un venit potential de `11090646.0`.
De asemenea, putem observa ca cel mai frecvent motiv cunoscut pentru anularea curselor este `Wrong Address`, cu `2348` curse anulare si cu o pierdere de venit potential de `972072.0`. Tinand cont de dimensiunea esantionului, nu este un lucru chiar atat de grav, este o greseala comuna si se poate intampla poate din cauza neatentiei, poate anumiti indivizi dau comenzi frecvente din diferite locatii si uita sa actualizeze locatia de preluare, poate checkpoint-ul de preluare este eronat din cauza conexiunii la internet sau diverse probleme tehnice. O rezolvare universala nu ar exista neaparat la acest motiv, insa s-ar putea lucra la imbunatatirea soft-ului din aplicatie si la adaugarea unui avertisment de atentie catre clienti atunci cand dau comanda, iar aceste lucruri probabil ar mai reduce semnificativ numarul de curse anulate din cauza gresirii adresei.

* 4.Compararea rating-urilor dintre șoferi și clienți, pe tip de vehicul.
![Screenshot from code query4](/Screenshot%20query4.png)
Am calculat media prin `AVG()` pentru `Driver Ratings` și `Customer Rating` și am grupat rezultatele pe tip de vehicul. Ordinea descrescătoare a clasamentului, pe baza rating-ului șoferilor, ne-a arătat ce tip de vehicul este cel mai apreciat de către clienți. Conform rezultatelor,`Uber XL` are un rating mediu al șoferilor de`4.238590`, sugerând că este cel mai apreciat de către clienți. O recomandare ar fi utilizarea unui număr cât mai mare de vehicule de acest tip, pentru o imagine de brand mai bună și o satisfacție sporită a clienților.

De asemenea, se observă faptul că rating-ul mediu primit de clienți de la șoferi `4.403978` este ceva mai ridicat decât cel primit de șoferi de la clienți. Această diferență, vizibilă pentru toate vehiculele, sugerează că șoferii sunt, în general, mai indulgenți cu clienții decât sunt clienții cu șoferii.

Cel mai puțin apreciat vehicul, conform rating-ului șoferilor, este `eBike`, cu un scor de `4.225571`. Deși diferența nu este semnificativă, mici îmbunătățiri ale serviciului pe acest segment ar putea fi benefice.

* 5.Distribuția veniturilor în funcție de metodele de plată.
Prin acest query am analizat distribuția veniturilor în funcție de metodele de plată. Conform rezultatelor, reiese faptul că metoda de plată `UPI` este de departe cea mai profitabilă, generând un venit total de `21104861.0`. Aceasta este urmată de plata cu `Cash`, cu un venit total de `11661552.0`, demonstrând o preferință clară pentru plățile digitale. Această analiză sugerează că firma ar trebui să continue să optimizeze și să promoveze sistemul `UPI` pentru a menține și a crește această sursă de venit.

### Concluzie
În concluzie, acest proiect a avut drept scop demonstrarea abilităților mele de prelucrare și analiză a datelor si in special cunostintele dobandite in lucrul cu bazele de date(SQL), utilizând un set de date real de pe Kaggle. Prin intermediul Python (Pandas) și SQL, am reușit să extrag informații valoroase și să transform datele brute în concluzii relevante pentru business, evidențiind cunoștințe practice în analiza datelor.

## Tehnologii folosite

* Python
* Pandas
* SQLite 
* Jupyter Notebook