# Cinnamon Tiling

Ekstenzija za Cinnamon (Linux Mint) koja donosi tiling prozora po rasporedima (layoutima), po uzoru na
[Tiling Shell](https://github.com/domferr/tilingshell) za GNOME. Napravljena za Cinnamon 6.x (X11 i Wayland).

## Funkcionalnosti

| Tiling Shell | Cinnamon Tiling |
|---|---|
| Tiling sistem: drži **Ctrl** dok vučeš prozor i spusti ga na tile | ✅ (tipku biraš u postavkama; može i "uvijek aktivno" + tipka za isključivanje) |
| Zauzimanje više tileova: drži **Alt** uz tiling sistem | ✅ |
| Snap assistant: povuci prozor prema vrhu ekrana i izaberi tile | ✅ (podesiva osjetljivost i animacija, opcija da izabrani layout postane aktivan) |
| Izbor layouta iz indikatora na panelu, po monitoru | ✅ (ikona indikatora prikazuje trenutni layout) |
| Grafički editor layouta (klik = podijeli, Ctrl+klik = podijeli vodoravno, desni klik = obriši, povlačenje razdjelnika) | ✅ + poništavanje (Ctrl+Z), Enter = spremi, Esc = odustani |
| Pametna promjena veličine (susjedni tileovi se mijenjaju zajedno) | ✅ |
| Tiling tipkovnicom (Super+strelice), širenje na susjedni tile, fokus po smjeru, sljedeći/prethodni, centriranje, odtilaj sve, mijenjanje layouta | ✅ (svi prečaci iz Tiling Shella) |
| Rubovi ekrana: lijevo/desno = polovina, uglovi = četvrtina, vrh = maksimiziraj; adaptivni način | ✅ |
| Gumbi za tiling u meniju prozora (desni klik na naslovnu traku) | ✅ (layouti + "Najbolji tile", "Krajnje lijevi/desni prazni tile", "Odtilaj") |
| Layout po radnom prostoru (workspaceu) | ✅ |
| Auto-tiling novih prozora | ✅ |
| Prijedlozi prozora za preostale prazne tileove | ✅ (tiling sistem, snap assistant, rubovi ekrana) |
| Obrub fokusiranog prozora | ✅ (širina, boja, radijus) |
| Zajedničko podizanje tiled prozora | ✅ |
| Razmaci (unutrašnji/vanjski) | ✅ |
| Vraćanje originalne veličine kad izvučeš prozor iz tilea | ✅ |
| Uvoz/izvoz layouta (JSON) | ✅ — **isti JSON format kao Tiling Shell**, layouti se mogu dijeliti |

Razlike u odnosu na GNOME verziju: nema zamućenja (blur) iza snap assistanta i nema zamjene Alt+Tab
prozora (Cinnamon nema odgovarajuće API-je), a radijus obruba se zadaje ručno umjesto da se računa
automatski.

## Instalacija

```bash
cp -r cinnamon-tiling@zelimir86 ~/.local/share/cinnamon/extensions/
```

Zatim **Sistemske postavke → Ekstenzije → Cinnamon Tiling → +** (ili `cinnamon-settings extensions`).
Postavke se otvaraju zupčanikom u istom prozoru ili iz menija indikatora na panelu.

## Sukobi s Cinnamonom

Dok je ekstenzija uključena:

* Cinnamonovo ugrađeno slaganje uz rub ekrana (`org.cinnamon.muffin edge-tiling`) se isključuje, jer bi
  se njegov Ctrl-snap sudarao s tiling sistemom.
* Cinnamonovi prečaci koji koriste iste tipke kao ova ekstenzija (po defaultu Super+strelice za
  `push-tile-*`) se privremeno uklanjaju.

Originalne vrijednosti se pamte i vraćaju kad isključiš ekstenziju. Oba ponašanja se mogu isključiti u postavkama.

## Struktura

```
cinnamon-tiling@zelimir86/
  extension.js          kontroler: postavke, layouti, prepisivanje Cinnamon postavki
  lib/layouts.js        model layouta, razmaci, spajanje/dijeljenje/brisanje tileova, razdjelnici
  lib/tilingManager.js  povlačenje prozora, rubovi ekrana, pametna promjena veličine, auto-tiling
  lib/snapAssist.js     snap assistant
  lib/editor.js         editor layouta
  lib/keybindings.js    tipkovničke akcije
  lib/suggestions.js    prijedlozi prozora
  lib/indicator.js      indikator na panelu i OSD za promjenu layouta
  lib/windowMenu.js     tiling sekcija u meniju prozora
  lib/windowBorder.js   obrub fokusiranog prozora
  lib/widgets.js        sličice layouta, pregledi
```

Logovi i greške: Looking Glass (`Alt+F2` → `lg`) ili `~/.xsession-errors`.
