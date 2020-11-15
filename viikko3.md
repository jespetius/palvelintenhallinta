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


