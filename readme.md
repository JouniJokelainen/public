## Git versiohallinnan käytöstä

Harmaalla pohjalla näkyvät komennot annetaan joko komentokehotteessa tai *Visual Studio Code*:n pääte (terminal) ikkunassa.  
Jos käytetään komentokehotetta, tulee työhakemistona olla 

Luodaan ensin uusi *Projekti* niminen kansio/hakemisto esim. *Tiedostot* hakemistoon.  
`md %userprofile%\documents`  

**Alustetaan työkansio Git:ä**

`git init ` | Alustetaan työhakemisto git käyttöä varten   
` git config --global user.email "you@example.com" `| Määrittää sähköpostiosoitteen    
` git config --global user.name "Etunimi Sukunimi"` | Määrittää käyttäjänimen    
`git config --list` | Näyttää asetukset  
`git config user.name` | Näyttää käyttäjän edellä määritetyn käyttäjänimen    
`git config --global init.defaultBranch main` | Muuttaa päähaaran nimeksi main masterin sijaan    
`git config --list --global` | Näyttää globaalit asetukset  
`git config --edit --global` | Avaa git asetukset oletuseditoriin. Oletuseditori valitaan alun perin gittiä asennettaessa)  

**Luodaan tiedosto a.txt ja sinne sisältöä**

Luodaan projekti hakemistoon uusi *a.txt*  niminen tiedosto.  Asetetaan sisällöksi *a* ja tallennetaan muutokset.  
`git add a.txt` | Lisätään a.txt indeksiin  
`git status` | Tarkistetaan gitin tilanne  
`git commit -m "Tiedosto a.txt luotu"` | Luodaan uusi committi    
`git log` | Tarkistetaan commitit  

**Luodaan tiedosto b.txt ja siihen sisältöä ja mutta vasta tässä vaiheessa "tajutaan" että se olisi pitänyt lisätä jo edelliseen commititin**

Luodaan *projekti* hakemistoon uusi *b.txt*  niminen tiedosto.  Asetetaan sisällöksi *b* ja tallennetaan muutokset.  
`git add b.txt` | Lisätään *b.txt* indeksiin  
`git status` | Tarkistetaan gitin tilanne    
`git commit --amend -m "Lisätty tiedosto A.txt ja B.txt"` | Lisätään indeksissä olevat tiedot eli uusi tiedosto *b.txt* edelliseen kommitiin ja muutetaan commitin komenttia    
`git log --oneline` |  Tarkistetaan git commitit tiiviimmässä muodossa 

**Luodaan tiedosto c.txt ja sinne sisältöä**

Luodaan projekti hakemistoon uusi *c.txt*  niminen tiedosto.  Asetetaan sisällöksi *c* ja tallennetaan muutokset.  
`git add .` | Lisätään tiedosto *c.txt* indeksiin..   
ja tajutaan että tiedostoa ei olisikaan vielä pitänyt lisätä indeksiin  
`git diff HEAD` |  Tarkistetaan mitä eroa on työkansiolla ja viimeksi commitoidulla tiedolla     
`git restore --staged c.txt` | Poistetaan tiedosto *c.txt* indkeksistä eli perutaan edellinen *add .* komento tiedoston *c.txt* osalta.  
`git status` | Tarkistetaan gitin tilanne. 

**Lisätään tiedosto d.txt ja siihen sisältöä**

Luodaan projekti hakemistoon uusi *d.txt*  niminen tiedosto.  Asetetaan sisällöksi *d* ja tallennetaan muutokset.  
`git add .` | Lisätään kaikki työkansion muutokset indeksiin.  Piste tarkoittaa kaikkia edellisen kommitin jälkeen tulleita muutoksia.     
`git commit -m "lisätty tiedostot c.txt ja d.txt"` | Luodaan uusi commit.    
`git log` | Tarkistetaan commitit  

**Lisätään lisää tietoa d.txt tiedostoon ja tallennetaan muutokset (ei commitoida)**

Lisätään tiedostoon *d.txt* uutta tietoa ja tallennetaan muutos.  
Huomataan että muutos halutaan perua.  
`git  checkout -- d.txt` | Palautetaan *d.txt* aiempaan versioon eli edellisessä commitissa olevaan tilanteeseen.      

**Luodaan uusi git haara eli branch**

`git branch` = Tarkastetaan nykyiset branchit.    
`git branch uusibranch` | Luodaan uusi branch TAI `git checkout -b uusibranch` | Luo ja siirtyy branchiin yhdellä komennolla.  
`git checkout uusibranch` | Siirrytään uuteen branchiin jos edellä ei käytetty komentoa *git checkout -b uusibranch*  

**Luodaan uusi tiedosto e.txt ja siihen sisältöä**

Luodaan uusi *e.txt* niminen tiedosto.  Asetetaan sisällöksi *e* ja tallennetaan muutokset.  
`git add e.txt` | Lisätään tiedosto *e.txt*  indeksiin.    
`git commit -m "Lisätty tiedosto e.txt"` | Luodaan uusi committi.    
`git log`   Tarkistetaan commitit.      
`git checkout main` |  Siirrytään takaisin *master* branchiin  
`git branch` | Tarkistetaan aktivinen branch    
`git merge uusibranch` | Yhdistetaan *master* ja *uusibranch haaroissa* olevat tiedot ja commitit.    

**Tarkastetaan että e.txt on ilmestynyt työkansioon ja poistetaan uusibranch** 

Tarkistetaan että tiedosto *e.txt* on ilmestynyt työhakemistoon.  

`git log` |  Tarkistetaan että edellä uusihaara branchissä luotu committi on lisätty *master* haaran kommitteihin.   
`git branch -d uusibranch` | Poistetaan edellä luotu *uusibranch* niminen branchi.    

**Tägääminen**:

`git tag v.1.0` | Lisää ns. *lifhtweight* tägin *v.1.0* joka tarttuu nykyiseen (mutta ei seuraaviin) kommittin.    

Luodaan uusi *y.txt* niminen tiedosto. Asetetaan sisällöksi *y* ja tallennetaan muutokset.     
`git add y.txt` | Lisätään tiedosto *y.txt* indeksiin.    
`git commit -m "Lisätty tiedosto y.txt` | Luodaan uusi committi.    
`git log --oneline` | Tarkistetaan git commitit tiiviissä muodossa.    
`git tag` | Tarkistetaan tägit.     

`git tag -a v.1.1 -m "Versio 1.1"` | Luodaan ns. *annotated täg*.     
`git show v.1.1` | Näyttää tägin *v.1.1*  
`git log --oneline` | Tarkistetaan git commitit tiiviissä muodossa   
`git tag v1.2` = luo tägin v.1.1 rinnalle    
`git log --oneline` | Tarkistetaan git commitit tiiviissä muodossa  
`git tag -d v1.2`| Poistetaan edellä luotu rinnakkainen v1.2 tägi    

**Tägit eivät kopioidu esim. Githubiin automaattisesti**   
Jos tägit halutaan kopioida esim. GitHub ympäristöön tulee ne siirtää sinne erikseen.  
`git push v.1.1` | Kopioi vain  kyseisen tägin.   
`git push tags` | Kopioi kaikki tägit    
`git push --delete v1.1` | Poistaa ko. tägin remotesta (esim. GitHub).    

#### Tiedostojen palauttamisesta: 

**Tallennettujen *commitoimattomien* tietojen peruminen**: 

Lisätään työkansioon tiedosto x.txt ja asetetaan sisällöksi *x* ja tallennetaan muutokset.  
`git add x.txt` Lisätään y.txt indeksiin.  
`git commit -m "Lisätty tiedosto x.txt"` | Luodaan uusi committi.    

Lisätään tiedostoon *x.txt* uutta sisältöä ja tallennetaan tiedosto
**HUOM**:  Ei committia eikä `add` tässä vaiheessa.  

Huomataan että uusi sisältö oli virhe ja halutaan palata tiedoston x.txt osalta aikaisempaan commitoituun sisältöön  
`git status` | Tarkistetaan gitin tilanne.     
`git checkout -- x.txt` | Palautetaan tiedosto *x.txt* edellisessä commitissa olevaan tilaan.      

**Tallennettujen ja commitoitujen tietojen peruminen**

Lisätään tiedostoon x.txt taas uutta sisältöä ja tallennetaan muutokset.  
`git commit -m "Sisältöä muokattu"` | Luodaan uusi commit joka sisätää edellä tehdyt muutokset.   

Huomataan että commitoitu sisältö oli virhe ja se halutaan perua. Tarkastetaan mitä muutoksia edellisessä commitissa oli.  

`git log --oneline` | Tulostetetaan commitit tiiviissä muodossa. Kopioidaan edellä tehdyn commitin id numero leikepöydälle.      
`git show *commitin id numero*` | Tarkistetaan mitä muutoksia committi sisältää.    
`git revert *peruttavan commitin id numero* --no-edit` | Perutaan viimeisimmässä commitissa olevat muutokset ja luodaan uusi committi perumisesta.   

**Työhakemistosta poistettun tiedoston palauttaminen**

Poistetaan tiedosto x.txt työhakemistosta.    
`git checkout HEAD x.txt` | Palauttaa edellä poistetun tiedoston x.txt työhakemistoon.    

Jos poistaminen olisi ehditty jo commitoida  
`git reset --hard HEAD~1` | Kumoaa viimeisimmän kommitin muutokset ja poistaa viimeisimmän commitin.  

#### Työhakemiston synkronoiminen GitHubiin

Rekisteröidytään GitHub ympäristöön ja käyttäjätunnusta ei vielä ole olemassa.  

`git branch -m main` | Vaihdetaan paikallisen *master* haaran nimeksi *main*.      

Luodaan uusi *projekti* niminen repositorio GitHubiin ja otetaan repositorion URL osoite leikepöydälle.  
`git remote add origin https://github.com/*oma github tunnus*/projekti.git` | Kytketään paikallinen työkansio Github repositorioon *origin* nimiseksi remoteksi.   

 `git remote -v` | Tarkastetaan että edellä luotu GitHub repositoria on kytketty remoteksi nimellä *origin*.    

Remote voidaan tarvittaessa nimetä uudelleen komennolla `git remote rename origin *uusi remoten nimi*`     

`git push -u origin main` | Pusketaan paikallinen projekti hakemiston sisältö Githubiin. 
Annetaan tarvittaessa GitHub käyttäjänimi ja salasana esille tulevaan ikkunaan.  
`git push origin --tags` | Pusketaan tägit GtiHubiin.    

Siirrytään GitHub ympäristöön ja lisätään sinne uusi *f.txt* niminen tiedosto.  GitHubissa ollaan yksi commit edellä  
`git fetch` | Haetaan GitHub tilanne paikalliseen ympäristöön.  
`git status` | Tarkistetaan gitin tilanne. Paikallinen ympäristö on yhden commitin (ja tiedoston) verran perässä GitHubissa olevan repositorian tilannetta.  
`git pull` | Kopioidaan GitHub:a olevat muutokset (tiedosto *f.txt* ja commit) paikalliseen työhakemistoon.    

Tarvittessa remote voidaan kytkeä irti komennolla remote `git remote rm origin`   

#### Upstream

Jos halutaan ladata sisältöä vieraasta *remotesta* oman työhakemistoon.  

Forkataan vieras julkinen repositorio omaan GitHubiin.   

Kloonataan oma forkki paikalliseksi työkansioksi.  

`git clone https://linkki_omaan_forkkiin.git`  

Lisätään paikallisen työkansioon upstream alkuperäiseen vieras repoon  
`git remote add upstream https://linkki_vieraaseen_repoon.git`  

`git remote -v`  

Alkuperäisessä etä_repossa on muutoksia ja ne pullataan paikalliseen työhakemistoon  

`git merge upstream/main`  

Tehdään muutoksia paikalliseen hakemistoon  

Lisätään ja commitoidaan  muutokset  
Työnnetään muutokset omaan forkkiin  
`git push` tai `git push origin`  

Luodaan *Pull request*  



