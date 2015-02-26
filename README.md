
# batch-rename

A simple Python script to **batch rename** files using **regular expressions.**
Tested on Linux, unlikely to work on other platforms. Use cautiously and backup your files if necessary. It is easy to do bad stuff with simple typos.

## Example usage

**TL;DR:** Python regexp replace (```re.subn```). Single quotes are your best friend.

The program asks you before doing anything (by default), so feel free to experiment.

Imagine you have an awesome music collection ripped from somewhere on the web. It looks all ugly like this:

```
Amor_latin_-_Samba_samba_(mp3.pm).mp3
Andrei_Freitas_-_Vamo_Samba_(mp3.pm).mp3
Arlindo_Cruz_e_Sombrinha_-_Hoje_Tem_Samba_SB_50_(mp3.pm).mp3
Art_Pepper_George_Cables_-_Samba_Mom_Mom_Samba_50_(mp3.pm).mp3
Avera_Feat._Me_You_-_Hoop_Loop_Samba_51_(mp3.pm).mp3
Ballroom_dance_-_Samba_samba_(mp3.pm).mp3
batuka_latin_-_chi-ki-cha_samba_samba_51_(mp3.pm).mp3
Bebel_Gilberto_-_Samba_De_Bencao_Samba_50_(mp3.pm).mp3
Bee_Gees_-_Stayin_Alive_Samba_(mp3.pm).mp3
Bellini_-_Mr._Samba_old_SB_50_(mp3.pm).mp3
# ... and 200 more files
```

Let's make it so your eyes do not bleed by looking at the names.

1. Replace underscores with braces:
```bash
rn _ ' '
```

2. Drop the ads in braces:
```bash
rn ' \(.*\)' ''
```

3. Fromat the dance and BPM information consistently.
```bash
rn '(.*) (Samba|samba|SB) ?([0-9]*)\.' '\1 (SB\3).'
```

4. A final touch: separate the BPM from the letters 'SB'.
```bash
rn '\(SB(.+)\)' '(SB \1)'
```

Finished! The files are now nicely and consistently named:

```
Amor latin - Samba (SB).mp3
Andrei Freitas - Vamo (SB).mp3
Arlindo Cruz e Sombrinha - Hoje Tem Samba (SB 50).mp3
Art Pepper George Cables - Samba Mom Mom (SB 50).mp3
Avera Feat. Me You - Hoop Loop (SB 51).mp3
Ballroom dance - Samba (SB).mp3
batuka latin - chi-ki-cha samba (SB 51).mp3
Bebel Gilberto - Samba De Bencao (SB 50).mp3
Bee Gees - Stayin Alive (SB).mp3
Bellini - Mr. Samba old (SB 50).mp3
```