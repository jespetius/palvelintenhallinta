# Palvelinten Hallinta Viikko 3

Tämä on palautus Palvelinten hallinta kurssille viikko 3.

a) MarkDown. Tee tämän tehtävän raportti MarkDownina

## d) Näytä omalla git-varastollasi esimerkit komennoista ‘git log’, ‘git diff’ ja ‘git blame’. Selitä tulokset.

	git log


commit b27aa78a60ef2a47a9e78afa93b8644eb570eb13 (HEAD -> main, origin/main, origin/HEAD)
Author: jespetius <jeppe.kuula@gmail.com>
Date:   Thu Nov 12 09:33:48 2020 +0200

    add time.py

commit 986af9d96a3ed00b94543379cd2bb13847fe1b07
Author: jespetius <jeppe.kuula@gmail.com>
Date:   Thu Nov 12 09:29:59 2020 +0200

    add hello.py

commit 662b7713a00f5e4164ffda288da5eed8c2cd0ad4
Author: jespetius <jeppe.kuula@gmail.com>
Date:   Thu Nov 12 09:26:09 2020 +0200

    typo fix

commit 62b9c15b453f2412d9cf9a31e376d0b6a77adfe8
Author: jespetius <jeppe.kuula@gmail.com>
Date:   Thu Nov 12 09:24:08 2020 +0200

    code directory

commit f4edc24e20d5a122a7aa8b349e18af2a1ac19bbd
Author: jespetius <jeppe.kuula@gmail.com>
Date:   Thu Nov 12 09:20:04 2020 +0200

    started coding

commit 6877d875edc20ecc758f918da18745635f4d6123
Author: jespetius <jeppe.kuula@gmail.com>
Date:   Thu Nov 12 08:54:50 2020 +0200

    first commit

commit 677351ead35865260be97e1896734f709ab6f6f7
Author: jespetius <54263238+jespetius@users.noreply.github.com>
Date:   Thu Nov 12 08:49:39 2020 +0200

    Initial commit

Nämä kaikki on minun tekemiä committeja tähän projektiin, jonka tein 12.11.2020 oppitunnilla.

	git diff viikko3.md

Tein juuri commitin, joten ei näy mitään. Kokeilen uudestaan:

	git diff viikko3.md

- git diff
+ git diff viikko3.md
+Tein juuri commitin, joten ei näy mitään. Kokeilen uudestaan:


git diff kertoo mikä ero nykyisellä ja edellisellä versiolla on.

	git blame viikko3.md

a1a3d433 (jespetius         2020-11-15 18:25:12 +0200  3) Tämä on palautus Palvelinten hallinta kurssille viikko 3.

Näyttää rivi kerrallaan kuka on kyseisen pätkän koodia tehnyt.


e) Tee tyhmä muutos gittiin, älä tee commit:tia. Tuhoa huonot muutokset ‘git reset –hard’. Huomaa, että tässä toiminnossa ei ole peruutusnappia.

Poistin kaikki rivit paitsi otsikon, jonka jälkeen tallensin tiedoston.
Annoin komennon:
	git reset --hard
Ja kaikki oli tallessa, mitä olin viimeksi puskenut githubiin.


f) Tee uusi salt-moduli. Voit asentaa ja konfiguroida minkä vain uuden ohjelman: demonin, työpöytäohjelman tai komentokehotteesta toimivan ohjelman. Käytä tarvittaessa ‘find -printf “%T+ %p\n”|sort’ löytääksesi uudet asetustiedostot. (Tietysti eri ohjelma kuin aiemmissa tehtävissä, tarkoitushan on harjoitella Salttia)
Aloitan puhtaalta pöydältä kokonaan. Ensiksi asennan orjan ja herran:
	sudo apt-get -y install salt-master salt-minion

Seuraavaksi menin minionin asetuksiin
	sudoedit /etc/salt/minion
 ja lisäsin asetustiedostoon seuraavat rivit
	master: 10.0.2.15
	id: jamesbond

Annoin seuraavat käskyt:

	sudo systemctl restart salt-minion.service 
	sudo salt-key -A
	y
	sudo salt '*' cmd.run 'whoami'

Sain vastaukseksi:
jamesbond:
    root

Sitten aloin työstämään moduulia:

	sudo mkdir -p /srv/salt/
	cd /srv/salt/
	sudo mkdir viikko3
	cd viikko3
	sudoedit init.sls

/tmp/viikko3.txt:
  file.managed:
    - source: salt://viikko3/viikko3.txt

	sudoedit viikko3.txt

Veckan 3

	sudo salt '*' state.apply viikko3


          ID: /tmp/viikko3.txt
    Function: file.managed
      Result: True
     Comment: File /tmp/viikko3.txt updated
     Started: 19:03:37.876816
    Duration: 34.354 ms
     Changes:   
              ----------
              diff:
                  New file
              mode:
                  0644

Summary for jamesbond
------------
Succeeded: 1 (changed=1)
Failed:    0
------------
Total states run:     1


Päätin että teen isomman  moduulin. Latasin kasan ohjelmia komennolla
	sudo apt -y install gimp neofetch htop speedcrunch

Testasin kaikki yksitellen:
	gimp
	neofetch
	htop	
	speedcrunch

Muokkasin init.sls

/tmp/viikko3.txt:
  file.managed:
    - source: salt://viikko3/viikko3.txt

downloads:
  pkg.installed:
    - name: gimp

Seuraavaksi testasin:
	sudo salt '*' state.apply viikko3


jamesbond:
----------
          ID: /tmp/viikko3.txt
    Function: file.managed
      Result: True
     Comment: File /tmp/viikko3.txt is in the correct state
     Started: 18:08:45.147133
    Duration: 76.192 ms
     Changes:   
----------
          ID: downloads
    Function: pkg.installed
        Name: gimp
      Result: True
     Comment: All specified packages are already installed
     Started: 18:08:50.382129
    Duration: 139.442 ms
     Changes:   

Summary for jamesbond
------------
Succeeded: 2
Failed:    0
------------
Total states run:     2
Total run time: 215.634 ms

lisäsin loputkin ohjelmat

downloads:
  pkg.installed:
    - pkgs:
      - gimp
      - neofetch
      - htop
      - speedcrunch

Vastaukseksi sain:

         ID: downloads
    Function: pkg.installed
      Result: True
     Comment: All specified packages are already installed
     Started: 18:19:22.034262
    Duration: 119.922 ms
     Changes:   

Summary for jamesbond
------------
Succeeded: 2
Failed:    0


Poistin kaikki ohjelmat komennolla:
	sudo apt autoremove  --purge htop gimp speedcrunch neofetch 
Testasin poistuiko kaikki oikeasti:
	gimp
Command 'gimp' not found, but can be installed with:

Seuraavaksi annoin komennon:
	sudo salt '*' state.apply viikko3


          ID: downloads
    Function: pkg.installed
      Result: True
     Comment: 4 targeted packages were installed/updated.
     Started: 18:27:48.919065
    Duration: 69386.806 ms



Summary for jamesbond
------------
Succeeded: 2 (changed=1)
Failed:    0
------------
Total states run:     2
Total run time:  69.457 s



