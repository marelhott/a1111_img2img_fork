# A1111 Img2Img Fork

Tato upravená verze populárního webového rozhraní **Automatic1111 Stable‑Diffusion WebUI** je zjednodušena tak, aby se soustředila pouze na režim *img2img*. Všechny ostatní záložky (například **txt2img**, **Extras**, **Train**, **Checkpoint Merger**, …) byly odstraněny a UI je nastaveno tak, aby při startu vždy zobrazovalo img2img.

## Zachované funkce

- **ControlNet** – Rozhraní pro nahrání a práci s ControlNet modely je součástí fork a je plně funkční.  Pokud nakopírujete modely do adresáře `models/ControlNet`, objeví se automaticky v nabídce.
- **Upscalery (LDSR/ScuNET/SwinIR)** – Integrované upscalery zůstaly zachovány.  V nastavení img2img můžete zvolit preferovaný algoritmus, popř. použít upscaling po generování.
- **LoRA** – Podpora LoRA modelů je dostupná prostřednictvím vestavěného rozšíření *Lora*.  LoRA soubory (.safetensors) ukládejte do `models/Lora`.
- **Advanced parametry** – Všechna nastavení img2img (velikost, denoising strength, batch size, CFG scale, samplery atd.) zůstala k dispozici.
- **Galerie náhledů** – Výstupní obrázky se zobrazují v přehlednější mřížce.  Každý řádek obsahuje čtyři náhledy a kliknutím na obrázek se zobrazí rychlý náhled ve větším okně.  Pod galerií jsou k dispozici tlačítka pro uložení/stažení obrázků nebo pro jejich odeslání zpět do img2img.

## Odebrané části

- Záložky **txt2img**, **Extras**, **Train**, **PNG Info**, **Checkpoint Merger** a **Extensions** byly odstraněny ze zobrazení.  Související soubory a skripty, které nesouvisely s img2img (např. prompt matrix, xyz grid, outpainting, postprocessing codeformer/gfpgan atd.) byly z repozitáře smazány.
- Vestavěná rozšíření nerelevantní k img2img (např. `extra-options-section`, `hypertile`, `mobile`, `postprocessing-for-training`, `prompt-bracket-checker`, `soft-inpainting`) byla rovněž odstraněna, aby se minimalizovala velikost a počet závislostí.

## Požadavky

- **Git** a **Python 3.10+** musí být nainstalovány v prostředí, kde budete aplikaci spouštět.
- Grafická karta s alespoň **8 GB** VRAM pro pohodlné generování (funguje i na 4 GB s omezeními).  ControlNet a některé upscalery mohou vyžadovat více paměti.

## Jak spustit na RunPod

1. V prostředí RunPod zvolte vhodný kontejner s podporou GPU (např. *PyTorch 2.1 + CUDA 12*).
2. Otevřete terminál a naklonujte tento fork:

   ```bash
   git clone https://github.com/<váš‑účet>/a1111_img2img_fork.git
   cd a1111_img2img_fork
   ```

   > **Poznámka:** Pokud repozitář teprve nahráváte na svůj GitHub, změňte URL podle svého uživatelského jména.  Soubor ZIP s celým projektem je rovněž k dispozici v sekci výstupu.

3. Spusťte skript `launch.sh`, který automaticky nainstaluje závislosti a spustí web UI:

   ```bash
   bash launch.sh --xformers
   ```

   Přepínač `--xformers` povoluje efektivnější VRAM management.  Pokud vám start selže, zkuste spustit bez něj.

4. Webové rozhraní se spustí na adrese `http://127.0.0.1:7860` (případně na jiné portu, pokud jej změníte pomocí parametru `--port`).

## Kam nahrát modely

- **Základní SD modely (.ckpt i .safetensors)** – ukládejte do `models/Stable-diffusion`.  Název souboru se automaticky objeví v rozbalovací nabídce „Checkpoint“ v pravém horním rohu UI.  Můžete mezi nimi přepínat bez restartu.
- **LoRA** – ukládejte do `models/Lora`.  V panelu „Extra networks“ uvnitř img2img klikněte na záložku *LoRA* a načtené modely budou k dispozici.
- **ControlNet modely** – ukládejte do `models/ControlNet`.  Po restartu UI se zobrazí v rozšíření ControlNet (obvykle jako první karta pod hlavním nastavením).  ControlNet umí pracovat se sd modely i LoRA zároveň.
- **Upscaler modely** – upscalery typu LDSR/ScuNET/SwinIR již mají potřebné modely v adresáři `extensions-builtin`, ale pokud chcete použít vlastní, vytvořte adresář `models/ESRGAN` a soubory (`.pth`) uložte tam.

Pokud používáte RunPod, doporučujeme tyto adresáře připojit jako *Persistent Volume*.  Díky tomu zůstanou modely zachovány mezi relacemi a není nutné je znovu nahrávat.

## Použití nové galerie náhledů

Výsledky img2img se zobrazují v galerii pod editačním panelem.  Galerie zobrazuje obrázky v mřížce o čtyřech sloupcích a umožňuje rychlé zobrazení většího náhledu – stačí kliknout na miniaturu.  Pod galerií najdete tlačítka pro stažení jednotlivých snímků, uložení všech obrázků do ZIPu nebo jejich odeslání zpět do formuláře img2img (např. pro další úpravy).

### Přizpůsobený vzhled

Tento fork obsahuje také úpravy rozložení a stylů inspirované moderními webovými aplikacemi. Rozhraní je rozděleno do dvou karet: vlevo je „karta“ pro nahrání vstupního obrázku a nastavení parametrů generování (model, sampler, CFG scale, kroky, denoise strength, rozměry, seed) a v pravé části je velký panel pro zobrazení výsledků. Tlačítko **Generovat obrázek** je zvýrazněno barevným přechodem a nepotřebné ovládací prvky („Interrupt“, „Skip“) jsou v img2img skryté. Textové pole pro zadání promptu a negativního promptu je pro zjednodušení ve výchozím stavu skryté; pokud potřebujete prompt zadat, můžete jej odkrýt úpravou CSS nebo přes API.

---

Pokud narazíte na jakýkoli problém s forkem nebo budete potřebovat další funkce, vytvořte issue ve svém repozitáři nebo upravte kód podle svých potřeb.  Celý projekt je open source a lze jej volně modifikovat.