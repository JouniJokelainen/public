## Git käyttö

Harmaalla pohjalla näkyvät komennot annetaan joko komentokehotteessa tai *Visual Studio Code*:n pääte (terminal) ikkunassa.  
Jos käytetään komentokehotetta, tulee työhakemistona olla 

Luodaan ensin uusi *Projekti* niminen kansio/hakemisto esim. *Tiedostot* hakemistoon.  
`md %userprofile%\documents`  

**Alustetaan työkansio Git:ä**

`git init `    alustetaan työhakemisto git käyttävarten   
` git config --global user.email "you@example.com" `  
` git config --global user.name "Your Name"`  
`git config --list` | näyttää asetukset  
`git config user.name` | (näyttää käyttäjän)  
`git config --global init.defaultBranch main` (muuttaa päähaaran nimeksi main masterin sijaan)  
`git config --list --global` | näyttää globaalit asetukset  
`git config --edit --global` | (avaa git asetukset oletuseditoriin. tämä valitaan alun perin gittiä asennettaessa)  

**Luodaan tiedosto a.txt ja sinne sisältöä**

`git add a.txt`  
`git status`  
`git commit -m "Tiedosto a.txt luotu"`  
`git log`  

**Luodaan tiedosto b.txt ja siihen sisältöä ja mutta vasta tässä vaiheessa "tajutaan" että se olisi pitänyt lisätä jo edelliseen commititin**

`git add b.txt`  
`git status`  
`git commit --amend` (muutetaan kommentointi sopivaksi ja tallennetaan) TAI ```git commit --amend -m "Lisätty tiedosto A.txt ja B.txt"```
`git log --oneline `

**Luodaan tiedosto c.txt ja sinne sisältöä**

`git add .` lisätään c.txt = seuraavaan indeksiin ja tajutaan että ei pitänytkään vielä lisätä  
`git diff HEAD` näyttää mitä eroa on työkansiolla ja viimeksi commitoidulla tiedolla    
`git restore --staged c.txt` tai  `git reset HEAD c.txt` = poistetaan tulevasta commitista eli perutaan edellinen add . c.txt tiedoston osalta.
`git status`

**Lisätään tiedosto d.txt ja siihen sisältöä**

`git add .`   
`git commit -m "lisätty tiedostot c.txt ja d.txt"` = lisätään ja suoritetaan commit"  
`git log`

**Lisätään lisää tietoa d.txt tiedostoon ja tallennetaan muutokset (ei commitoida)**

`git  checkout -- d.txt` = palautetaan d.txt aiempaan versioon (edelliseen kommittiin)    
**HUOM**: git revert *commit hash* = peruu hashissä/commitissa tehdyt muutokset tiedostoihin  

**Luodaan uusi branch**

`git branch` = tarkastetaan puu  
`git branch uusibranch` = luodaan uus branch TAI ``git checkout -b uusibranch`` (luo ja siirtyy branchiin samointein)
`git checkout uusibranch` = siirrytään uuteen branchiin

**Luodaan uusi tiedosto e.txt ja siihen sisältöä**

`git add e.txt` = lisätään seuraavaan committiin  
`git commit -m "Lisätty tiedosto e.txt"` luodaan commit  
`git log`   
`git checkout main` = siirrytään master branchiin  
`git branch` = tarkastetaan branch  
`git merge uusibranch` = yhdistetään haarat  

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



