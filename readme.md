## Git versiohallinnan käytöstä

**Git:n asentaminen**  

Varmista että olet asentanut Git ohjelmiston. Voit asentaa Git:n oletusasetuksin. Git:n voit ladata [täältä](https://git-scm.com/install/).  
Avaa komentokehote (*cmd.exe*) aja anna komento `git`. 
Jos git on asennettu oikein, edellinen komento tulostaa näytölle ohjeita git:n käytöstä.   
Jos komento palauttaa ilmoituksen tuntemattomasta komennosta, sulje kaikki komentokehoteikkunat ja mahdolliset ohjelmointieditorit. Avaa komentotulkki ja kokeile komentoa uudelleen.  

**Projekti aloittaminen**  

Luodaan komentokehotteessa uusi *Projekti* niminen kansio/hakemisto esim. *Tiedostot* hakemistoon.  
`md %userprofile%\documents`  

Harmaalla pohjalla näkyvät komennot annetaan joko komentokehotteessa tai *Visual Studio Code*:n pääte (terminal) ikkunassa.  
Jos käytetään komentokehotetta, tulee työhakemistona olla *C:\users\omatunnus\Documents\Tiedostot\Projekti*.  

**Alustetaan työkansio Git:ä**

`git init ` | Alustetaan työhakemisto git käyttöä varten   
`git config --global user.email "etunimi.sukunimi@example.com" `| Määrittää sähköpostiosoitteen    
`git config --global user.name "Etunimi Sukunimi"` | Määrittää käyttäjänimen    
`git config --list` | Näyttää asetukset  
`git config user.name` | Näyttää käyttäjän edellä määritetyn käyttäjänimen    
`git config --global init.defaultBranch main` | Muuttaa pääkehityshaaran nimeksi *main* masterin sijaan (jos pääkehityshaaran nimi on *master*)    
`git config --list --global` | Näyttää globaalit eli kaikille git alustetuille hakemistoille yhteiset asetukset  
`git config --edit --global` | Avaa git asetukset oletuseditoriin. Oletuseditori valitaan alun perin gittiä asennettaessa)  

**Tiedosto .gitignore**  

.gitignore tiedoston avulla määritellään mitkä tiedostotyypit ja hakemistot jätetään git versiohallinnan ulkopuolelle.
Luodaan *projekti* hakemistoon uusi tiedosto nimeltä *.gitignore*   
Luodaan *projekti* hakemistoon uusi hakemisto nimeltä *alustava*  
Luodaan uusi *suunnitelma.txt* niminen tiedosto hakemistoon *alustava*   
Haluamme jättää *alustava* hakemiston sisältöineen git versiohallinnan ulkpuolelle
Asetetaan *.gitignore* tiedoston sisällöksi seuraavaa *alustava/* ja tallennetaan muutokset       

`git add .` | Lisätään tiedosto *.gitignore* indeksiin  
`git status` | Tarkistetaan gitin tilanne  
`git commit -m "Tiedosto .gitignore luotu"` | Luodaan ensimmäinen committi/muutos    

**Luodaan tiedosto a.txt ja sinne sisältöä**

Luodaan projekti hakemistoon uusi *a.txt*  niminen tiedosto.  Asetetaan sisällöksi *a* ja tallennetaan tiedosto.  
`git add a.txt` | Lisätään a.txt indeksiin  
`git status` | Tarkistetaan gitin tilanne  
`git commit -m "Tiedosto a.txt luotu"` | Luodaan uusi committi/muutos    
`git log` | Tarkistetaan commitit/muutokset  

**Luodaan uusi tiedosto b.txt ja siihen sisältöä. Haluamme lisätä tiedoston b.txt jo edellä luotuun commititin/muutokseen**

Luodaan *projekti* hakemistoon uusi *b.txt*  niminen tiedosto.  Asetetaan sisällöksi *b* ja tallennetaan tiedosto.  
`git add b.txt` | Lisätään *b.txt* indeksiin  
`git status` | Tarkistetaan gitin tilanne    
`git commit --amend -m "Lisätty tiedosto A.txt ja B.txt"` | Lisätään indeksissä olevat tiedot eli uusi tiedosto *b.txt* edelliseen kommitiin ja muutetaan commitin/muutoksen kommenttia    
`git log --oneline` |  Tarkistetaan git commitit/muutokset tiiviimmässä muodossa 

**Luodaan uusi tiedosto c.txt ja siihen sisältöä**

Luodaan projekti hakemistoon uusi *c.txt*  niminen tiedosto.  Asetetaan sisällöksi *c* ja tallennetaan tiedosto.  
`git add .` | Lisätään tiedosto *c.txt* indeksiin..   
ja tajutaan että tiedostoa ei olisi vielä pitänyt lisätä indeksiin  
`git diff HEAD` |  Tarkistetaan mitä eroa on työkansiolla ja viimeksi commitoidulla eli viimeisessä muutoksessa olevilla tiedolla     
`git restore --staged c.txt` | Poistetaan tiedosto *c.txt* indeksistä eli perutaan edellinen *add .* komento tiedoston *c.txt* osalta.  
`git status` | Tarkistetaan gitin tilanne. 

**Lisätään uusi tiedosto d.txt ja siihen sisältöä**

Luodaan projekti hakemistoon uusi *d.txt*  niminen tiedosto.  Asetetaan sisällöksi *d* ja tallennetaan tiedosto.  
`git add .` | Lisätään kaikki työkansion muutokset indeksiin.  Piste tarkoittaa kaikkia edellisen commitin/muutoksen jälkeen kansioon tulleita muokkauksia/lisäyksiä.     
`git commit -m "lisätty tiedostot c.txt ja d.txt"` | Luodaan uusi commit/muutos.    
`git log` | Tarkistetaan commitit/muutokset  

**Lisätään lisää tietoa d.txt tiedostoon ja tallennetaan tiedoston muokkaus (ei commitoida/tehdä uutta muutosta). Tallenetut muokkaukset tiedostoon halutaan perua**

Lisätään tiedostoon *d.txt* uutta tietoa ja tallennetaan muutokset tiedostoon.  
Huomataan että tiedostoon tehdyt muokkaukset halutaan perua.  
`git  checkout -- d.txt` | Palautetaan *d.txt* aiempaan versioon eli edellisessä commitissa/muutoksessa olevaan tilanteeseen.      

**Luodaan uusi muutoshaara eli branch**

`git branch` = Tarkastetaan nykyiset muutoshaarat/branchit.    
`git branch bugfixi` | Luodaan uusi muutoshaara/branch TAI `git checkout -b bugfixi` | Luo ja siirtyy muutoshaaraan bugfixi yhdellä komennolla.  
`git branch -m bugfixi bugfix` | muutetaan muutoshaaran nimi bugfixi -> bugfix  
`git checkout bugfix` TAI `git switch bugfix` | Siirrytään uuteen muutoshaaraan jos edellä ei käytetty komentoa *git checkout -b bugfix*    

**Luodaan bugfix muutoshaaraan uusi tiedosto e.txt ja siihen sisältöä**

Luodaan uusi *e.txt* niminen tiedosto.  Asetetaan sisällöksi *e* ja tallennetaan muutokset tiedostoon.  
Tarkastetaan että ollaan *bugfix* muutoshaarassa ja tarvittaessa siirrytään *bugfix* muutoshaaraan.   
`git add e.txt` | Lisätään tiedosto *e.txt*  indeksiin.    
`git commit -m "Lisätty tiedosto e.txt"` | Luodaan uusi committi.    
`git log`   Tarkistetaan commitit/muutokset.      
`git checkout main` |  Siirrytään takaisin *main* muutoshaaraan  
`git branch` | Tarkistetaan aktivinen muutoshaara    
`git merge bugfix` | Yhdistetaan *main* ja *bugfix* haaroissa olevat tiedot ja commitit/muutokset.    

**Tarkastetaan että tiedosto e.txt on ilmestynyt työkansioon main muutoshaarassa ja poistetaan muutoshaara bugfix** 

Tarkistetaan että tiedosto *e.txt* on ilmestynyt työhakemistoon.  

`git log` |  Tarkistetaan että edellä *bugfix* muutoshaarassa luotu committi/muutos on lisätty *main* muutoshaaran committien/muutosten jatkoksi.   
`git branch -d bugfix` | Poistetaan edellä luotu *bugfix* niminen muutoshaara.    

**Työhakemiston sisällön tarkastelu halutussa commitissa/muutoksessa**   

`git log --oneline` |  Listataan commitit/muutokset ja otetaan jonkin commitin/muutoksen id/hash leikepöydälle.    
`git checkout *commit id*` | Siirrytään haluttuun committiin/muutokseen sen id-/hash numeron avulla    
Työhakemiston sisältö päivittyy vastaamaan työhakemiston tilannetta committin/muutoksen ottamisen hetkellä.    
`git chekcout main` | siirrytään takaisin viimeisimmän commitin/muutoksen mukaiseen tilanteeseen työhakemistossa.    

**Tägien luominen, tarkastelu ja poistaminen**:  

`git tag v.1.0` | Lisää ns. *lightweight* tägin *v.1.0* joka tarttuu nykyiseen (mutta ei seuraaviin) committin/muutoksen.    

Luodaan uusi *y.txt* niminen tiedosto. Asetetaan sisällöksi *y* ja tallennetaan tiedosto.     
`git add y.txt` | Lisätään tiedosto *y.txt* indeksiin.    
`git commit -m "Lisätty tiedosto y.txt` | Luodaan uusi committi/muutos.    
`git log --oneline` | Tarkistetaan git commitit tiiviissä muodossa.    
`git tag` | Tarkistetaan tägit.    
`git log` v.1.0 --oneline` | Näyttää commitit/muutokset jotka edeltävät mainittua tagiä    

`git tag -a v.1.1 -m "Versio 1.1"` | Luodaan ns. *annotated tag*.     
`git show v.1.1` | Näyttää tägin *v.1.1*  
`git log --oneline` | Tarkistetaan git commitit tiiviissä muodossa   
`git tag v1.2` = luo tägin v.1.1 rinnalle    
`git log --oneline` | Tarkistetaan git commitit/muutokset tiiviissä muodossa  
`git tag -d v1.2`| Poistetaan edellä luotu rinnakkainen v1.2 tägi    

**Tägit eivät kopioidu esim. Githubiin automaattisesti**   

Jos tägit halutaan kopioida esim. GitHub ympäristöön tulee ne kopioida sinne erikseen.  
`git push v.1.1` | Puskee vain kyseisen tägin.   
`git push --tags` | Puskee kaikki tägit GtiHub:n    
`git push --delete v1.1` | Poistaa ko. tägin remotesta (esim. GitHub).    

#### Tiedostojen palauttamisesta: 

**Tallennettujen mutta *commitoimattomien*/muutosten ulkopuolella olevin muokkausten peruminen**: 

Lisätään työkansioon uusi tiedosto *x.txt* ja asetetaan sisällöksi *x* ja tallennetaan muutokset tiedostoon.  
`git add x.txt` | Lisätään tiedosto *x.txt* indeksiin.  
`git commit -m "Lisätty tiedosto x.txt"` | Luodaan uusi committi/muutos tiedoston *x.txt* tilasta.    

Lisätään tiedostoon *x.txt* uutta sisältöä ja tallennetaan tiedostoon tehdyt muutokset  
**HUOM**:  Ei uutta committia/muutosta eikä `add` tässä vaiheessa.  

Huomataan että muutokset tiedostoon *x.txt* perua ja palata tiedoston *x.txt* osalta aikaisempaan commitoituun/muutoksessa olevaan sisältöön  
`git status` | Tarkistetaan gitin tilanne.     
`git checkout -- x.txt` | Palautetaan tiedosto *x.txt* uusimmassa commitissa/muutoksessa olevaan tilaan.      

**Tallennettujen ja commitoitujen/muutokseen tallenenttujen tietojen peruminen**

Lisätään jälleen tiedostoon *x.txt* taas uutta sisältöä ja tallennetaan muutokset tiedostoon.  
`git commit -m "Tiedostoa x.txt muokattu"` | Luodaan uusi commit/muutos joka sisältää edellä tehdyt muutokset tiedostoon.   

Huomataan että jo commitoidut/muutokseen lisätyt muokkauset tiedostoon *x.tx* oli virhe ja ne halutaan perua. Tarkastetaan ensin mitä muutoksia edellisessä commitissa/muutoksssa oli.  

`git log --oneline` | Tulostetetaan commitit/muutokset tiiviissä muodossa. Kopioidaan edellä tehdyn commitin/muutoksen id/hash numero leikepöydälle.      
`git show *commitin id numero*` | Tarkistetaan mitä tietoja committi/muutos sisältää.    
`git revert *peruttavan commitin id numero* --no-edit` | Perutaan viimeisimmässä commitissa/muutoksessa olevat muokkaukset tiedostoon ja luodaan uusi committi/muutos perumisesta. Tässä yhteydessä luodun commitin/muutoksen avaulla voimme vielä kumota edellisen *git revert* komennon ja sen aiheuttamat muutokset tiedostoon.      

**Työhakemistosta poistettun tiedoston palauttaminen**

Poistetaan tiedosto *x.txt* työhakemistosta.    
`git checkout HEAD x.txt` TAI `git checkout -- x.txt` | Palautetaan edellä poistetettu edoston *x.txt* takaisin työhakemistoon.    
 
Jos poistaminen olisi ehditty jo commitoida/tallentaa muutokseen    
`git reset --hard HEAD~1` tai `git revert --no-edit *Poiston commitID*` | Kumoaa viimeisimmän kommitin muutokset ja poistaa viimeisimmän commitin/muutoksen.  


**Commitin/muutoksen poistaminen eli muutoshistorian muokkaaminen**
Halutaan poistaa viimeisin commit/muutos.  
Luodaan työhakemistoon uusi tiedosto *y.txt* ja asetetaan sisällöksi *y*.  
`git add y.txt` | Lisätään tiedosto *y.txt* indeksiin.  
`git commit -m "Lisätty tiedosto y.txt"` | Luodaan uusi commit/muutos joka sisältää tiedoston *y.txt* ja sen sisällön.   
`git log --oneline` | Tarkastetaan commitit/muutokset tiiviissä muodossa.  
Todetaan että tiedosto commitoitiin/tehtiin muutos liian aikaisin ja halutaan perua viimeisin commitin/muutos mutta säästää muutokset työhakemistossa.   
`git reset --soft HEAD~1` | Commit/muutos poistetaan muutoshistoriasta mutta tiedoston tilaa ei palauteta edelliseen tilaan.        

Jos haluamme siis ainoastaan poistaa commitin/muutoksen mutta säästää muutokset työkansiossa
`git reset --soft *commit hash*` TAI `git reset --soft HEAD~1`   

*** HUOM Älä käytä *git reset* komentoa jos olet jakanut projektin muille esim. GitHub:a.***   

#### Työhakemiston synkronoiminen GitHubiin    

Rekisteröidytään GitHub ympäristöön ja käyttäjätunnusta ei vielä ole olemassa.  
`git branch -m main` | Vaihdetaan paikallisen *master* haaran nimeksi *main*. (Jos tätä ei vielä ole tehty)      

Luodaan uusi *projekti* niminen repositorio GitHubiin ja otetaan repositorion URL osoite leikepöydälle.  
`git remote add origin https://github.com/*oma github tunnus*/projekti.git` | Kytketään paikallinen työkansio Github repositorioon *origin* nimiseksi remoteksi.   

`git remote -v` | Tarkastetaan että edellä luotu GitHub repositoria on kytketty remoteksi nimellä *origin*.    

Remote voidaan tarvittaessa nimetä uudelleen komennolla `git remote rename origin *uusi remoten nimi*`     

`git push -u origin main` | Pusketaan paikallinen *projekti* työhakemiston sisältö Githubiin. (*git push origin --all* puskee kaikki paikalliset haarat GitHubiin)  
Annetaan tarvittaessa GitHub käyttäjänimi ja salasana esille tulevaan ikkunaan.  
`git push origin --tags` | Pusketaan myös olemassa olevat tägit GtiHubiin.    

Siirrytään GitHub ympäristöön ja lisätään sinne uusi *f.txt* niminen tiedosto ja tallenetaan tiedosto tekemällä GitHubissa commit/muutos.  GitHubissa ollaan nyt yksi commit/muutos edellä paikallista työhakemistoa  
`git fetch` | Tarkastetaan GitHub tilanne ja verrataan sitä paikalliseen ympäristöön/työhakemistoon.  
`git status` | Tarkistetaan gitin tilanne. Paikallinen ympäristö on yhden commitin/muutoksen (ja tiedoston) verran jäljessä GitHubissa olevan repositorian tilannetta.  
`git pull` | Kopioidaan GitHub:a olevat muutokset (tiedosto *f.txt* ja commit/muutos) paikalliseen työhakemistoon.    

Tarvittessa *remote* voidaan kytkeä irti komennolla `git remote rm origin`   

#### Upstream
Upstream on GitHub repositoria josta voidaan hakea sisältöjä, committeja/muutoksia paikallisen työhakemistoon. Tyypillisesti upstream on jonkun toisen henkilön omistuksessa oleva GitHub repositorio josta halutaan hakea muutoksia suoraan paikalliseen työhakemistoon.

Forkataan/kopioidaan jokin vieras julkinen repositorio omaan GitHubiin.   
`git clone https://linkki_omaan_forkkiin.git` | Kloonataan edellä luotu forkki paikalliseksi työkansioksi.      
`git remote add upstream https://linkki_vieraaseen_repoon.git`| Lisätään paikallisen työkansioon upstream alkuperäiseen vieras repoon  
`git remote -v` | Tarkistetaan etähakemistojen/repojen tilanne    

Kun alkuperäisessä etärepoon tulee muutoksia ne voidaan vetää/pullata suoraan paikalliseen työhakemistoon ohi oman forkin  
`git merge upstream/main` | Vedetään muutokset upstream etähakemistosta/reposta paikalliseen hakemistoon     

Tehdään muutoksia paikalliseen hakemistoon, lisätään ja commitoidaan  muutokset  
Työnnetään muutokset omaan forkkiin  
`git push` tai `git push origin`  

Luodaan *Pull request*  



