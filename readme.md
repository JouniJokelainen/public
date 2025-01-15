## Git käyttö

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

Luodaan projekti hakemistoon uusi *a.txt*  niminen tiedosto.  
`git add a.txt` | Lisätään a.txt indeksiin  
`git status` | Tarkistetaan gitin tilanne  
`git commit -m "Tiedosto a.txt luotu"` | Luodaan uusi committi    
`git log` | Tarkistetaan commitit  

**Luodaan tiedosto b.txt ja siihen sisältöä ja mutta vasta tässä vaiheessa "tajutaan" että se olisi pitänyt lisätä jo edelliseen commititin**

Luodaan *projekti* hakemistoon uusi *b.txt*  niminen tiedosto.  
`git add b.txt` | Lisätään *b.txt* indeksiin  
`git status` | Tarkistetaan gitin tilanne    
`git commit --amend -m "Lisätty tiedosto A.txt ja B.txt"` | Lisätään indeksissä olevat tiedot eli uusi tiedosto *b.txt* edelliseen kommitiin ja muutetaan commitin komenttia    
`git log --oneline` |  Tarkistetaan git commitit tiiviimmässä muodossa 

**Luodaan tiedosto c.txt ja sinne sisältöä**

Luodaan projekti hakemistoon uusi *c.txt*  niminen tiedosto.  
`git add .` | Lisätään tiedosto *c.txt* indeksiin..   
ja tajutaan että tiedostoa ei olisikaan vielä pitänyt lisätä indeksiin  
`git diff HEAD` |  Tarkistetaan mitä eroa on työkansiolla ja viimeksi commitoidulla tiedolla     
`git restore --staged c.txt` | Poistetaan tiedosto *c.txt* indkeksistä eli perutaan edellinen *add .* komento tiedoston *c.txt* osalta.  
`git status` | Tarkistetaan gitin tilanne. 

**Lisätään tiedosto d.txt ja siihen sisältöä**

Luodaan projekti hakemistoon uusi *d.txt*  niminen tiedosto.  
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

Luodaan uusi *e.txt* niminen tiedosto.  
`git add e.txt` | Lisätään tiedosto *e.txt*  indeksiin.    
`git commit -m "Lisätty tiedosto e.txt"` | Luodaan uusi committi.    
`git log`   Tarkistetaan commitit.      
`git checkout main` |  Siirrytään takaisin *master* branchiin  
`git branch` | Tarkistetaan aktivinen branch    
`git merge uusibranch` | Yhdistetaan *master* ja *uusibranch haaroissa* olevat tiedot ja commitit.    

**Tarkastetaan että e.txt on ilmestynyt työkansioon ja poistetaan uusibranch** 

`git branch -d uusibranch` = poistetaan sivuhaara  

**Tägääminen**:

Merkitsee työhakemiston nykyisen tilan tägillä joka tarttuu nykyiseen (mutta ei seuraaviin) kommittin  
`git tag v.1.0` = luo lightweight tägin jossa ei ole tietoja  

Luodaan esim. y.txt  
`git add .`  
`git commit -m "Lisätty tiedosto y.txt`  
`git log --oneline`  
`git tag` = näyttää tägit  

`git tag -a v.1.1 -m "Versio 1.1"` = luo ns. annotated tägin josta voidaan kaivaa tietoja `git show v.1.1` komennolla  
`git show v.1.1`  
`git log --oneline`  
`git tag 1.2` = luo tägin v.1.1 rinnalle = halutaan poistaa se  
`git log --oneline`
`git tag -d v1.2`  

**Tägit eivät siirry esim. Githubiin automaattisesti**   
`git push v.1.1` = siirtää vain  kyseisen tägin  
`git push tags` = siirtää kaikki tägit  
`git push --delete v1.1` = poistaa ko. tägin remotesta  

#### Tiedostojen palauttamisesta: 

**Tallennettujen *commitoimattomien* tietojen peruminen**: 

Lisätään työkansioon tiedosto x.txt vaikkapa VScodella ja sisällöksi X ja tallennetaan

`git add .`  
`git commit -m "Lisätty tiedosto X.txt"`  

Lisätään tiedostoon X.txt väärää sisältöä ja tallennetaan tiedosto | **HUOM**:  Ei committia eikä `add` tässä välissä

Lisätään tiedostoon X.txt uutta sisältöä esim. ZZZ ja tallennetaan.

Huomataan että uusi sisältö oli virhe ja halutaan palata tiedoston X.txt osalta aikaisempaan commitoituun sisältöön  
`git status`   
`git checkout -- X.txt`    

**Tallennettujen ja commitoitujen tietojen peruminen**

Lisätään tiedostoon X.txt uutta sisältöä ZXZX ja tallennetaan muutokset  
Kommitoidaan muutos  
`git commit -m "Sisältöä muokattu"` (em. komento ei toimi tiedostoissa joita ei aiemmin ole jo lisätty git add komenolla)

Huomataan että uusi commitoitu sisältö oli virhe ja se halutaan perua. Tarkastetaan mitä muutoksia commitissa oli

`git log --oneline`  
`git show *commitin id numero*`  
`git revert *peruttavan commitin id numero*` TAI `git revert *peruttavan commitin id numero* --no-edit` (jolloin perumisen aiheuttamaa commit viestiä ei muokata)

**Työhakemistosta poistettun tiedoston palauttaminen**

`del X.txt`  
`git checkout HEAD x.txt`  

**HUOM** jos poistaminen olisi ehditty jo commitoida  
`git reset --hard HEAD~1` = kumoaa viimeisimmän kommitin muutokset ja poistaa viimeisimmän kommitin  

#### Työhakemiston synkronoiminen GitHubiin

Vaihdetaan paikallisen *master* haaran nimi *main* nimiseksi  
`git branch -m main`  

Luodaan repositorio GitHubiin ja otetaan repositorion URL osoite leikepöydälle  
`git remote add origin https://github.com/AzureandGit/githarjoitus.git` = kytketään paikallinen työkansio Github repositorioon  

Tarkastetaan etärepositorio =  `git remote -v`  

**HUOM:** Remote voidaan uudelleen nimetä komennolla `git remote rename origin github`   

Pusketaan paikallinen työkansio Githubiin =  `git push -u origin main`  
Pusketaan tägit = `git push origin --tags`  
Listätään Githubin kautta tiedosto = GitHubissa ollaan yksi commit edellä  
Haetaan githubin tilanne = `git fetch`  
Synkronoidaan githubin tilanne paikalliseen työkansioon = `git pull`  
Poisteaan remote `git remote rm origin`   

#### Upstream

Jos halutaan ladata sisältöä vieraasta *remotesta* oman työhakemistoon

Forkataan vieras julkinen repositorio omaan GitHubiin

Kloonataan oma forkki paikalliseksi työkansioksi

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



