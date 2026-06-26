# Invaders — PET Disassembly & C64 Port

**Invaders** è il classico gioco *Space Invaders* (stile Taito 1978) disassemblato per **Commodore PET** da Dave McMurtrie (Agosto 2023).  
Questo repository contiene:

- `invaders.asm` — Disassemblaggio completo del gioco originale per PET
- `invaders_c64.asm` — Versione adattata per **Commodore 64** (TODO)

## Storia

Il gioco originale fu scritto per il Commodore PET con il kit di espansione **SuperPET** (che aggiungeva l'hardware VIA per il suono).  
Il disassemblaggio è stato ricostruito a partire dal binario PET, recuperando tutte le strutture dati, gli sprite in caratteri PETSCII e la mappa del livello "How To Get Sound".

## Come girava su PET

- **Indirizzo**: caricato a `$0401` con un BASIC loader `SYS 1039`
- **Memoria video**: `$8000–$83FF` (1000 byte, 40×25)
- **Suono**: VIA 6522 a `$E810`–`$E84B` (shift register + timer per effetti sonori)
- **Joystick/input**: PIA 6520 a `$E810`/`$E812`
- **Interrupt**: software tramite vettori in zero page `$0090`–`$0093`

## Porting su Commodore 64

Le differenze principali tra PET e C64:

| Aspetto          | PET                | C64                    |
|------------------|--------------------|------------------------|
| Video            | `$8000`            | `$0400`                |
| Colore           | assente            | `$D800`                |
| Character ROM   | PET graphics       | C64 PETSCII            |
| VIA/PIA          | `$E8xx`            | CIA `$DCxx` / SID `$D4xx` |
| IRQ vector       | `$0090/$0091`      | `$0314/$0315`          |
| CRSRBLNK         | `$E458` (kernal)   | `$E458` (kernal) — uguale |

## Controlli di gioco (originali PET)

| Tasto | Azione                |
|-------|-----------------------|
| `A`   | Muovi a sinistra      |
| `D`   | Muovi a destra        |
| `J`   | Fuoco                 |

## Crediti

- Disassemblaggio originale: **Dave McMurtrie** `<dave@commodore.international>`
- Adattamento C64: **a cura di questo progetto**
