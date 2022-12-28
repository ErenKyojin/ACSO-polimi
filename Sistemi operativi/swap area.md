---
alias: swap file
---

File o partizione del disco che consiste in una sequenza di Page Slot di dimensione pari ad una pagine
- **SWPN (Swap Page Number)** identifica un page slot
- Ogni page slot ha un contatore **swap_map_counter**
Per tenere traccia del numero di PTE riferiti alla pagina fisica swappata sul disco