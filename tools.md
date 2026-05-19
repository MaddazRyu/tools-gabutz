# ╔════════════════════════════════════════════════════════════════════════════╗
# ║   🚀 GONDRONG TOOLS - MEGA PLATFORM: AI + NON-AI TOOLS                     ║
# ║   Dibuat oleh: MaddazXD - Gondrong STIES                                   ║
# ║   AI Models: Claude Sonnet 4.6 & Claude Opus 4.7 (pilihan user)           ║
# ║   Platform: Puter.js (gratis, tanpa API key)                              ║
# ║   Stack: React + TypeScript + Vite + TailwindCSS                          ║
# ║   Total Tools: 600+ AI Tools + 250+ Non-AI Tools (850+ total)            ║
# ╚════════════════════════════════════════════════════════════════════════════╝

---

## � INSTRUKSI UTAMA UNTUK REPLIT AI AGENT

Kamu adalah senior full-stack developer. Tugasmu adalah membangun **Gondrong Tools** — sebuah website platform tools raksasa dengan **600+ AI Tools** dan **250+ Non-AI Tools** yang bisa langsung dipakai di browser.

*Dibuat dengan ❤️ oleh **MaddazXD - Gondrong STIES***

**WAJIB DIBACA SEBELUM MULAI:**
1. Baca SEMUA instruksi ini sampai selesai
2. Buat SEMUA file secara paralel — jangan skip satu pun
3. Setiap file harus FULLY FUNCTIONAL — tidak ada placeholder, tidak ada TODO
4. User bisa MEMILIH model AI: `claude-opus-4-6` atau `claude-sonnet-4-6`
5. Tools Non-AI harus berjalan 100% offline (tanpa Puter, tanpa API)
6. Footer WAJIB ada link "Powered by Puter" → https://developer.puter.com
7. Model AI yang tersedia: **Claude Sonnet 4.6** (cepat) dan **Claude Opus 4.7** (powerful)
8. Buat SEMUA file yang disebutkan secara parallel
9. Credit: Built on top of Puter.js platform

---

## SETUP GLOBAL (WAJIB DIPAHAMI DULU)

### index.html - Tambahkan di <head>:
```html
<script src="https://js.puter.com/v2/"></script>
```

### Cara panggil Claude via Puter.js (WAJIB pakai format ini):
```typescript
// Non-streaming:
const res = await window.puter.ai.chat(prompt, { model: "claude-opus-4-7" });
const text: string = res.message.content[0].text;

// Streaming:
const stream = await window.puter.ai.chat(prompt, { model: "claude-opus-4-7", stream: true });
for await (const chunk of stream) {
  const piece = chunk?.text ?? "";
}

// Generate Gambar:
const imgEl = await window.puter.ai.txt2img(prompt, { model: "gpt-image-2" });

// Text to Speech:
const audio = await window.puter.ai.txt2speech(text, { provider: "openai" });

// Speech to Text:
const result = await window.puter.ai.speech2txt(file);
const transcript = result.text;

// OCR:
const text = await window.puter.ai.img2txt(imageFile);
```

### TypeScript global type (tambahkan di src/types/puter.d.ts):
```typescript
declare global {
  interface Window {
    puter: {
      ai: {
        chat: (
          prompt: string | object[],
          options?: {
            model?: string;
            stream?: boolean;
            temperature?: number;
            max_tokens?: number;
          }
        ) => Promise<any>;
        txt2img: (prompt: string, options?: { model?: string; test_mode?: boolean }) => Promise<HTMLImageElement>;
        txt2speech: (
          text: string,
          options?: { provider?: string; voice?: string; language?: string }
        ) => Promise<HTMLAudioElement>;
        txt2vid: (prompt: string, options?: { test_mode?: boolean }) => Promise<any>;
        img2txt: (file: File | string) => Promise<string>;
        speech2txt: (
          file: File | Blob,
          options?: { model?: string; language?: string; translate?: boolean }
        ) => Promise<{ text: string }>;
        speech2speech: (
          file: File | Blob,
          options?: { voice?: string }
        ) => Promise<any>;
        listModels: () => Promise<any[]>;
        listModelProviders: () => Promise<any[]>;
        txt2speech: {
          listEngines: () => Promise<any[]>;
          listVoices: (provider?: string) => Promise<any[]>;
        } & ((text: string, options?: object) => Promise<HTMLAudioElement>);
      };
      fs: {
        write: (path: string, data: any, options?: { overwrite?: boolean; dedupeName?: boolean }) => Promise<any>;
        read: (path: string) => Promise<Blob>;
        readdir: (path: string) => Promise<any[]>;
        delete: (path: string, options?: { recursive?: boolean }) => Promise<void>;
        upload: (file: File | File[], path?: string) => Promise<any>;
        getReadURL: (path: string) => Promise<string>;
        mkdir: (path: string, options?: { dedupeName?: boolean }) => Promise<any>;
        copy: (src: string, dst: string, options?: { overwrite?: boolean }) => Promise<void>;
        move: (src: string, dst: string, options?: { overwrite?: boolean }) => Promise<void>;
        rename: (path: string, newName: string) => Promise<any>;
        stat: (path: string) => Promise<any>;
      };
      kv: {
        set: (key: string, value: any, options?: { ttl?: number }) => Promise<void>;
        get: (key: string) => Promise<any>;
        del: (key: string) => Promise<void>;
        list: (pattern?: string, options?: { values?: boolean }) => Promise<any[]>;
        flush: () => Promise<void>;
        incr: (key: string, amount?: number) => Promise<number>;
        decr: (key: string, amount?: number) => Promise<number>;
        add: (key: string, value: any, path?: string) => Promise<void>;
        remove: (key: string, path?: string) => Promise<void>;
        update: (key: string, updates: Record<string, any>) => Promise<void>;
      };
      auth: {
        signIn: () => Promise<void>;
        signOut: () => Promise<void>;
        isSignedIn: () => boolean;
        getUser: () => Promise<{ username: string; uuid: string; email?: string }>;
        getMonthlyUsage: () => Promise<any>;
        getDetailedAppUsage: (appName: string) => Promise<any>;
      };
      hosting: {
        create: (subdomain: string, dirPath: string) => Promise<any>;
        list: () => Promise<any[]>;
        delete: (subdomain: string) => Promise<void>;
        update: (subdomain: string, dirPath: string) => Promise<void>;
        get: (subdomain: string) => Promise<any>;
      };
      workers: {
        create: (name: string, file: File) => Promise<any>;
        delete: (name: string) => Promise<void>;
        list: () => Promise<any[]>;
        get: (name: string) => Promise<any>;
        exec: (name: string, args?: any) => Promise<any>;
      };
      apps: {
        create: (options: object) => Promise<any>;
        list: () => Promise<any[]>;
        delete: (name: string) => Promise<void>;
        update: (name: string, options: object) => Promise<any>;
        get: (name: string) => Promise<any>;
      };
    };
  }
}
export {};
```

---

## 📦 SETUP PROYEK

### package.json
```json
{
  "name": "gondrong-tools",
  "version": "1.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "tsc && vite build",
    "preview": "vite preview"
  },
  "dependencies": {
    "react": "^18.3.1",
    "react-dom": "^18.3.1",
    "lucide-react": "^0.400.0",
    "zustand": "^4.5.2",
    "fuse.js": "^7.0.0"
  },
  "devDependencies": {
    "@types/react": "^18.3.3",
    "@types/react-dom": "^18.3.0",
    "@vitejs/plugin-react": "^4.3.1",
    "autoprefixer": "^10.4.19",
    "postcss": "^8.4.39",
    "tailwindcss": "^3.4.6",
    "typescript": "^5.5.3",
    "vite": "^5.3.4"
  }
}
```

### index.html — WAJIB include Puter.js di <head>
```html
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Gondrong Tools — 850+ Tools Gratis | MaddazXD</title>
  <meta name="description" content="Platform 850+ tools gratis: AI dengan Puter.js + 250+ tools non-AI offline. Dibuat oleh MaddazXD - Gondrong STIES. Pilih model AI sesukamu!">
  <!-- WAJIB: Puter.js SDK -->
  <script src="https://js.puter.com/v2/"></script>
</head>
<body class="bg-gray-950 text-white">
  <div id="root"></div>
  <script type="module" src="/src/main.tsx"></script>
</body>
</html>
```

---

## 🗂️ STRUKTUR FOLDER LENGKAP

```
gondrong-tools/
├── .git
├── .gitignore
├── index.html
├── package.json
├── vite.config.ts
├── tailwind.config.js
├── tsconfig.json
├── postcss.config.js
│
└── src/
    ├── main.tsx
    ├── App.tsx
    │
    ├── types/
    │   └── puter.d.ts           ← TypeScript types untuk Puter.js
    │
    ├── store/
    │   ├── useAppStore.ts       ← Zustand store: navigasi, model AI, theme
    │   ├── toolRegistry.ts      ← Daftar semua 850+ tools
    │   └── useToolStore.ts      ← Store untuk tool-specific state
    │
    ├── lib/
    │   ├── puter.ts             ← Wrapper semua fungsi Puter.js
    │   ├── utils.ts             ← Helper umum (copy, format, dll)
    │   ├── localUtils.ts        ← Utility untuk tools non-AI (lokal)
    │   └── constants.ts         ← Konstanta global
    │
    ├── components/
    │   ├── Layout/
    │   │   ├── Sidebar.tsx      ← Sidebar navigasi kiri
    │   │   ├── Header.tsx       ← Header + model selector
    │   │   ├── Footer.tsx       ← Footer dengan "Powered by Puter"
    │   │   └── ToolContainer.tsx← Wrapper setiap tool
    │   │
    │   └── UI/
    │       ├── Button.tsx
    │       ├── Input.tsx
    │       ├── Textarea.tsx
    │       ├── Select.tsx
    │       ├── Card.tsx
    │       ├── Badge.tsx
    │       ├── Spinner.tsx
    │       ├── Toast.tsx
    │       ├── Modal.tsx
    │       ├── ProgressBar.tsx
    │       ├── CopyButton.tsx
    │       ├── FileUpload.tsx
    │       ├── StreamOutput.tsx
    │       ├── ModelSelector.tsx ← FITUR: pilih claude-opus-4-6 atau claude-sonnet-4-6
    │       ├── ToolBadge.tsx    ← Badge "AI" atau "Local"
    │       └── SearchBar.tsx
    │
    ├── pages/
    │   ├── HomePage.tsx         ← Halaman utama dengan grid semua tools
    │   ├── CategoryPage.tsx     ← Halaman per kategori
    │   └── ToolPage.tsx         ← Wrapper render tool aktif
    │
    ├── tools/
    │   ├── writing/             ← 52 tools AI untuk menulis
    │   ├── content/             ← 55 tools AI konten kreator
    │   ├── image/               ← 32 tools AI gambar
    │   ├── audio/               ← 28 tools AI audio
    │   ├── video/               ← 22 tools AI video
    │   ├── developer/           ← 62 tools (mix AI + lokal)
    │   ├── seo/                 ← 42 tools AI SEO
    │   ├── social/              ← 48 tools AI sosial media
    │   ├── productivity/        ← 50 tools (mix AI + lokal)
    │   ├── education/           ← 40 tools AI pendidikan
    │   ├── business/            ← 42 tools (mix AI + lokal)
    │   ├── data/                ← 30 tools (mix AI + lokal)
    │   ├── health/              ← 20 tools AI kesehatan
    │   ├── legal/               ← 20 tools AI hukum
    │   ├── finance/             ← 22 tools (mix AI + lokal)
    │   ├── fun/                 ← 25 tools AI hiburan
    │   │
    │   └── local/               ← ⭐ KATEGORI BARU: 250+ TOOLS NON-AI
    │       ├── text/            ← 50 tools teks offline
    │       ├── converter/       ← 60 tools konverter offline
    │       ├── generator/       ← 40 tools generator offline
    │       ├── calculator/      ← 50 tools kalkulator offline
    │       ├── formatter/       ← 30 tools formatter offline
    │       └── utility/         ← 30 tools utility offline
```

---

## ⚙️ CORE FILES WAJIB

### src/types/puter.d.ts
```typescript
declare global {
  interface Window {
    puter: {
      ai: {
        chat: (
          prompt: string | object[],
          options?: {
            model?: string;
            stream?: boolean;
            temperature?: number;
            max_tokens?: number;
          }
        ) => Promise<any>;
        txt2img: (prompt: string, options?: { model?: string; test_mode?: boolean }) => Promise<HTMLImageElement>;
        txt2speech: (
          text: string,
          options?: { provider?: string; voice?: string; language?: string }
        ) => Promise<HTMLAudioElement>;
        txt2vid: (prompt: string, options?: { test_mode?: boolean }) => Promise<any>;
        img2txt: (file: File | string) => Promise<string>;
        speech2txt: (
          file: File | Blob,
          options?: { model?: string; language?: string; translate?: boolean }
        ) => Promise<{ text: string }>;
        speech2speech: (
          file: File | Blob,
          options?: { voice?: string }
        ) => Promise<any>;
        listModels: () => Promise<any[]>;
        listModelProviders: () => Promise<any[]>;
        txt2speech: {
          listEngines: () => Promise<any[]>;
          listVoices: (provider?: string) => Promise<any[]>;
        } & ((text: string, options?: object) => Promise<HTMLAudioElement>);
      };
      fs: {
        write: (path: string, data: any, options?: { overwrite?: boolean; dedupeName?: boolean }) => Promise<any>;
        read: (path: string) => Promise<Blob>;
        readdir: (path: string) => Promise<any[]>;
        delete: (path: string, options?: { recursive?: boolean }) => Promise<void>;
        upload: (file: File | File[], path?: string) => Promise<any>;
        getReadURL: (path: string) => Promise<string>;
        mkdir: (path: string, options?: { dedupeName?: boolean }) => Promise<any>;
        copy: (src: string, dst: string, options?: { overwrite?: boolean }) => Promise<void>;
        move: (src: string, dst: string, options?: { overwrite?: boolean }) => Promise<void>;
        rename: (path: string, newName: string) => Promise<any>;
        stat: (path: string) => Promise<any>;
      };
      kv: {
        set: (key: string, value: any, options?: { ttl?: number }) => Promise<void>;
        get: (key: string) => Promise<any>;
        del: (key: string) => Promise<void>;
        list: (pattern?: string, options?: { values?: boolean }) => Promise<any[]>;
        flush: () => Promise<void>;
        incr: (key: string, amount?: number) => Promise<number>;
        decr: (key: string, amount?: number) => Promise<number>;
        add: (key: string, value: any, path?: string) => Promise<void>;
        remove: (key: string, path?: string) => Promise<void>;
        update: (key: string, updates: Record<string, any>) => Promise<void>;
      };
      auth: {
        signIn: () => Promise<void>;
        signOut: () => Promise<void>;
        isSignedIn: () => boolean;
        getUser: () => Promise<{ username: string; uuid: string; email?: string }>;
        getMonthlyUsage: () => Promise<any>;
        getDetailedAppUsage: (appName: string) => Promise<any>;
      };
      hosting: {
        create: (subdomain: string, dirPath: string) => Promise<any>;
        list: () => Promise<any[]>;
        delete: (subdomain: string) => Promise<void>;
        update: (subdomain: string, dirPath: string) => Promise<void>;
        get: (subdomain: string) => Promise<any>;
      };
      workers: {
        create: (name: string, file: File) => Promise<any>;
        delete: (name: string) => Promise<void>;
        list: () => Promise<any[]>;
        get: (name: string) => Promise<any>;
        exec: (name: string, args?: any) => Promise<any>;
      };
      apps: {
        create: (options: object) => Promise<any>;
        list: () => Promise<any[]>;
        delete: (name: string) => Promise<void>;
        update: (name: string, options: object) => Promise<any>;
        get: (name: string) => Promise<any>;
      };
    };
  }
}
export {};
```

### src/store/useAppStore.ts — ZUSTAND STORE (Model Selector WAJIB)
```typescript
import { create } from "zustand";
import { persist } from "zustand/middleware";

export type AIModel = "claude-sonnet-4-6" | "claude-opus-4-7";

export interface AppState {
  // Navigation
  activeToolId: string;
  activeCategoryId: string;
  setActiveToolId: (id: string) => void;
  setActiveCategoryId: (id: string) => void;

  // AI Model selection (FITUR UTAMA)
  selectedModel: AIModel;
  setSelectedModel: (model: AIModel) => void;

  // Search
  searchQuery: string;
  setSearchQuery: (q: string) => void;

  // Sidebar
  sidebarOpen: boolean;
  setSidebarOpen: (open: boolean) => void;
  expandedCategories: string[];
  toggleCategory: (id: string) => void;

  // History (simpan ke Puter KV)
  favorites: string[];
  toggleFavorite: (toolId: string) => void;
  recentTools: string[];
  addRecentTool: (toolId: string) => void;
}

export const useAppStore = create<AppState>()(
  persist(
    (set, get) => ({
      activeToolId: "",
      activeCategoryId: "",
      setActiveToolId: (id) => {
        set({ activeToolId: id });
        get().addRecentTool(id);
      },
      setActiveCategoryId: (id) => set({ activeCategoryId: id }),

      // Default model: claude-sonnet-4-6 (lebih cepat & efisien)
      selectedModel: "claude-sonnet-4-6" as AIModel,
      setSelectedModel: (model: AIModel) => set({ selectedModel: model }),

      searchQuery: "",
      setSearchQuery: (q) => set({ searchQuery: q }),

      sidebarOpen: true,
      setSidebarOpen: (open) => set({ sidebarOpen: open }),

      expandedCategories: [],
      toggleCategory: (id) => {
        const current = get().expandedCategories;
        set({
          expandedCategories: current.includes(id)
            ? current.filter((c) => c !== id)
            : [...current, id],
        });
      },

      favorites: [],
      toggleFavorite: (toolId) => {
        const current = get().favorites;
        set({
          favorites: current.includes(toolId)
            ? current.filter((id) => id !== toolId)
            : [...current, toolId],
        });
      },

      recentTools: [],
      addRecentTool: (toolId) => {
        const current = get().recentTools.filter((id) => id !== toolId);
        set({ recentTools: [toolId, ...current].slice(0, 10) });
      },
    }),
    { name: "gondrong-tools-store" }
  )
);
```

### src/lib/puter.ts — WRAPPER HELPER (Dengan Model Selector)
```typescript
import { useAppStore } from "../store/useAppStore";

// Ambil model aktif dari store
export function getActiveModel(): string {
  return useAppStore.getState().selectedModel;
}

// Chat biasa (non-streaming)
export async function aiChat(prompt: string, modelOverride?: string): Promise<string> {
  const model = modelOverride ?? getActiveModel();
  const res = await window.puter.ai.chat(prompt, { model });
  return res.message.content[0].text;
}

// Chat streaming (untuk output panjang)
export async function* aiStream(prompt: string, modelOverride?: string): AsyncGenerator<string> {
  const model = modelOverride ?? getActiveModel();
  const stream = await window.puter.ai.chat(prompt, { model, stream: true });
  for await (const chunk of stream) {
    yield chunk?.text ?? "";
  }
}

// Multi-turn chat (dengan history)
export async function* aiStreamWithHistory(
  messages: { role: "user" | "assistant"; content: string }[],
  modelOverride?: string
): AsyncGenerator<string> {
  const model = modelOverride ?? getActiveModel();
  const stream = await window.puter.ai.chat(messages, { model, stream: true });
  for await (const chunk of stream) {
    yield chunk?.text ?? "";
  }
}

// Generate gambar
export async function generateImage(prompt: string): Promise<HTMLImageElement> {
  return window.puter.ai.txt2img(prompt, { model: "gpt-image-2" });
}

// Text to Speech
export async function textToSpeech(
  text: string,
  options?: { provider?: string; voice?: string }
): Promise<HTMLAudioElement> {
  return window.puter.ai.txt2speech(text, { provider: "openai", ...options });
}

// Speech to Text
export async function speechToText(file: File, translate = false): Promise<string> {
  const result = await window.puter.ai.speech2txt(file, { translate });
  return result.text;
}

// OCR: Gambar ke Teks
export async function imageToText(file: File): Promise<string> {
  return window.puter.ai.img2txt(file);
}

// KV Store helpers
export async function kvSet(key: string, value: any): Promise<void> {
  await window.puter.kv.set(key, JSON.stringify(value));
}

export async function kvGet<T>(key: string): Promise<T | null> {
  try {
    const val = await window.puter.kv.get(key);
    return val ? JSON.parse(val) : null;
  } catch {
    return null;
  }
}

export async function kvDel(key: string): Promise<void> {
  await window.puter.kv.del(key);
}

// File System helpers
export async function fsWrite(path: string, data: string): Promise<void> {
  await window.puter.fs.write(path, data, { overwrite: true });
}

export async function fsRead(path: string): Promise<string> {
  const blob = await window.puter.fs.read(path);
  return await blob.text();
}

// Auth helpers
export function isSignedIn(): boolean {
  return window.puter.auth.isSignedIn();
}

export async function signIn(): Promise<void> {
  await window.puter.auth.signIn();
}
```

### src/components/UI/ModelSelector.tsx — KOMPONEN WAJIB
```tsx
import { useAppStore, AIModel } from "../../store/useAppStore";

const MODELS: { value: AIModel; label: string; desc: string; badge: string }[] = [
  {
    value: "claude-sonnet-4-6",
    label: "Claude Sonnet 4.6",
    desc: "Cepat & efisien — cocok untuk sehari-hari & tugas umum",
    badge: "⚡ Cepat",
  },
  {
    value: "claude-opus-4-7",
    label: "Claude Opus 4.7",
    desc: "Paling powerful & akurat — cocok untuk tugas kompleks & demanding",
    badge: "🧠 Powerful",
  },
];

export default function ModelSelector() {
  const { selectedModel, setSelectedModel } = useAppStore();

  return (
    <div className="flex items-center gap-2">
      <span className="text-gray-400 text-xs whitespace-nowrap">Model AI:</span>
      <div className="flex bg-gray-800 rounded-lg p-0.5 gap-0.5">
        {MODELS.map((m) => (
          <button
            key={m.value}
            onClick={() => setSelectedModel(m.value)}
            title={m.desc}
            className={`px-3 py-1.5 rounded-md text-xs font-medium transition-all duration-200 ${
              selectedModel === m.value
                ? "bg-violet-600 text-white shadow-lg shadow-violet-900/50 scale-105"
                : "text-gray-400 hover:text-white hover:bg-gray-700"
            }`}
          >
            {m.badge} {m.value === "claude-opus-4-7" ? "Opus" : "Sonnet"}
          </button>
        ))}
      </div>
    </div>
  );
}
```

---

## DAFTAR LENGKAP SEMUA TOOLS (600+ AI + 250+ Local = 850+ total)

### ══════════════════════════════════
### KATEGORI 1: ✍️ TOOLS MENULIS (52 tools)
### ══════════════════════════════════
# File: src/tools/writing/

01. ArticleWriter.tsx         - Buat artikel blog panjang dari topik
02. BlogPostGenerator.tsx     - Generator postingan blog SEO-friendly
03. EssayWriter.tsx           - Penulis esai akademik/formal
04. StoryWriter.tsx           - Penulis cerita fiksi/cerpen
05. NovelChapter.tsx          - Generator bab novel
06. ScriptWriter.tsx          - Penulis skrip film/YouTube/podcast
07. Paraphraser.tsx           - Parafrasa teks agar berbeda
08. Summarizer.tsx            - Ringkasan teks panjang
09. GrammarChecker.tsx        - Koreksi tata bahasa
10. SpellChecker.tsx          - Koreksi ejaan
11. ToneChanger.tsx           - Ubah nada tulisan (formal/casual/friendly)
12. TextExpander.tsx          - Perluas teks pendek jadi panjang
13. TextShortener.tsx         - Persingkat teks panjang
14. ParagraphWriter.tsx       - Buat paragraf dari ide
15. IntroductionWriter.tsx    - Buat kalimat/paragraf pembuka
16. ConclusionWriter.tsx      - Buat kesimpulan dari teks
17. HeadlineGenerator.tsx     - Buat judul yang menarik
18. SubheadingGenerator.tsx   - Buat sub-judul konten
19. MetaDescWriter.tsx        - Buat meta deskripsi SEO
20. ProductDescription.tsx    - Deskripsi produk e-commerce
21. BioWriter.tsx             - Buat bio profil (Instagram/LinkedIn/Twitter)
22. CoverLetter.tsx           - Surat lamaran kerja
23. ResumeWriter.tsx          - Buat resume/CV
24. EmailWriter.tsx           - Buat email profesional
25. EmailReply.tsx            - Balas email dengan AI
26. EmailSubjectLine.tsx      - Buat subject email yang menarik
27. NewsletterWriter.tsx      - Buat konten newsletter
28. PressRelease.tsx          - Buat siaran pers
29. ProposalWriter.tsx        - Buat proposal bisnis/proyek
30. ReportWriter.tsx          - Buat laporan formal
31. MeetingNotes.tsx          - Rangkum catatan meeting
32. MemoWriter.tsx            - Buat memo internal
33. PolicyWriter.tsx          - Buat kebijakan/SOP
34. JobDescription.tsx        - Buat deskripsi lowongan kerja
35. PerformanceReview.tsx     - Buat penilaian kinerja karyawan
36. ThankYouNote.tsx          - Buat ucapan terima kasih
37. ApologyLetter.tsx         - Buat surat permintaan maaf
38. ComplaintLetter.tsx       - Buat surat keluhan
39. RecommendationLetter.tsx  - Buat surat rekomendasi
40. PoemWriter.tsx            - Buat puisi dari tema
41. LyricsWriter.tsx          - Buat lirik lagu
42. JokeGenerator.tsx         - Buat lelucon/humor
43. QuoteGenerator.tsx        - Buat kutipan inspiratif
44. MottoGenerator.tsx        - Buat motto/tagline
45. SloganGenerator.tsx       - Buat slogan brand
46. CTAWriter.tsx             - Buat Call-to-Action yang convert
47. LandingPageCopy.tsx       - Teks halaman landing page
48. AboutUsWriter.tsx         - Buat halaman "Tentang Kami"
49. FAQGenerator.tsx          - Buat daftar FAQ
50. TestimonialWriter.tsx     - Buat testimonial palsu realistis
51. TranslatorTool.tsx        - Terjemahan ke 100+ bahasa
52. LanguageDetector.tsx      - Deteksi bahasa teks

### ══════════════════════════════════
### KATEGORI 2: 🎬 TOOLS KONTEN KREATOR (55 tools)
### ══════════════════════════════════
# File: src/tools/content/

53. ViralAnalyzer.tsx         - Analisis timestamp viral YouTube
54. YouTubeScriptWriter.tsx   - Buat skrip video YouTube
55. YouTubeTitleGenerator.tsx - Buat judul YouTube yang clickbait
56. YouTubeDescWriter.tsx     - Buat deskripsi video YouTube
57. YouTubeTagsGenerator.tsx  - Buat tags/keyword YouTube
58. YouTubeThumbnailIdea.tsx  - Ide desain thumbnail YouTube
59. YouTubeHookWriter.tsx     - Buat hook 3 detik pembuka video
60. YouTubeEndscreen.tsx      - Skrip penutup/outro video
61. TikTokScriptWriter.tsx    - Buat skrip video TikTok
62. TikTokHookGenerator.tsx   - Buat hook TikTok yang viral
63. TikTokCaptionWriter.tsx   - Buat caption TikTok + hashtag
64. TikTokTrendAnalyzer.tsx   - Analisis tren TikTok dari topik
65. InstagramCaptionWriter.tsx- Buat caption Instagram
66. InstagramBioWriter.tsx    - Buat bio Instagram
67. InstagramHashtags.tsx     - Generator hashtag Instagram relevan
68. InstagramCarouselScript.tsx- Skrip konten carousel Instagram
69. ReelsScriptWriter.tsx     - Skrip video Reels
70. PodcastOutlineWriter.tsx  - Buat outline episode podcast
71. PodcastIntroWriter.tsx    - Buat intro podcast
72. PodcastShowNotes.tsx      - Buat show notes podcast
73. PodcastQuestions.tsx      - Buat pertanyaan wawancara podcast
74. ContentCalendar.tsx       - Buat kalender konten 30 hari
75. ContentIdeasGenerator.tsx - Generator 100 ide konten
76. NicheAnalyzer.tsx         - Analisis niche yang profitable
77. CompetitorAnalysis.tsx    - Analisis kompetitor konten
78. AudiencePersona.tsx       - Buat persona audiens target
79. StorytellingFramework.tsx - Framework cerita untuk konten
80. ViralHookFormulas.tsx     - 50 formula hook viral
81. ContentRepurposer.tsx     - Ubah 1 konten jadi 10 format
82. ThreadWriter.tsx          - Buat Twitter/X thread
83. LinkedInPostWriter.tsx    - Buat postingan LinkedIn
84. LinkedInArticleWriter.tsx - Buat artikel LinkedIn panjang
85. FacebookPostWriter.tsx    - Buat postingan Facebook
86. WhatsAppBroadcast.tsx     - Buat pesan broadcast WhatsApp
87. TelegramPost.tsx          - Buat konten channel Telegram
88. PinterestDescription.tsx  - Buat deskripsi pin Pinterest
89. ProductReviewWriter.tsx   - Buat review produk
90. UnboxingScript.tsx        - Skrip video unboxing
91. TutorialScriptWriter.tsx  - Skrip video tutorial
92. MotivationalContent.tsx   - Konten motivasi/inspirasi
93. MemeTextGenerator.tsx     - Buat teks meme
94. ClickbaitTitle.tsx        - Generator judul clickbait
95. StorytellingPost.tsx      - Buat konten storytelling
96. BeforeAfterContent.tsx    - Format konten before/after
97. ListicleWriter.tsx        - Buat artikel daftar (listicle)
98. CaseStudyWriter.tsx       - Buat studi kasus
99. InterviewQnA.tsx          - Format konten Q&A
100. MiniCoursOutline.tsx     - Buat outline mini kursus
101. ChallengeIdeas.tsx       - Ide challenge viral
102. GiveawayPost.tsx         - Buat postingan giveaway
103. PollQuestions.tsx        - Buat pertanyaan polling
104. AMAQuestions.tsx         - Buat pertanyaan AMA (Ask Me Anything)
105. SponsoredContentWriter.tsx- Buat konten sponsored/iklan
106. AffiliateCopyWriter.tsx  - Buat copy konten affiliate
107. ReviewResponseWriter.tsx - Balas ulasan/komentar negatif

### ══════════════════════════════════
### KATEGORI 3: 🖼️ TOOLS GAMBAR (32 tools)
### ══════════════════════════════════
# File: src/tools/image/

108. ImageGenerator.tsx       - Generate gambar dari teks (gpt-image-2)
109. LogoConceptGenerator.tsx - Buat konsep/prompt logo
110. ThumbnailGenerator.tsx   - Generate thumbnail YouTube
111. BannerGenerator.tsx      - Generate banner iklan
112. SocialMediaImageGen.tsx  - Generate gambar sosmed berbagai size
113. ProductMockupPrompt.tsx  - Prompt untuk mockup produk
114. InfographicPrompt.tsx    - Prompt untuk infografis
115. IllustrationPrompt.tsx   - Prompt ilustrasi karakter
116. BackgroundRemoverDesc.tsx- Deskripsi cara hapus background
117. ImagePromptEnhancer.tsx  - Perbaiki prompt gambar agar lebih baik
118. StableDiffusionPrompt.tsx- Buat prompt Stable Diffusion
119. MidjourneyPrompt.tsx     - Buat prompt Midjourney
120. DALLEPromptWriter.tsx    - Buat prompt DALL-E optimal
121. ImageAltTextWriter.tsx   - Buat alt text gambar untuk SEO
122. ImageCaptionWriter.tsx   - Buat caption untuk gambar
123. ImageAnalyzer.tsx        - Analisis isi gambar (OCR + deskripsi)
124. PhotoEditingIdeas.tsx    - Ide editing foto untuk konten
125. ColorPaletteGenerator.tsx- Generate palet warna dari deskripsi
126. FontPairingAdvisor.tsx   - Rekomendasi pasangan font
127. DesignFeedback.tsx       - Feedback desain dari deskripsi
128. BrandIdentityGuide.tsx   - Buat panduan identitas brand
129. IconPromptGenerator.tsx  - Prompt untuk icon set
130. PatternPromptGenerator.tsx- Prompt untuk pattern/tekstur
131. WallpaperPrompt.tsx      - Prompt wallpaper
132. BookCoverPrompt.tsx      - Prompt cover buku
133. AlbumCoverPrompt.tsx     - Prompt sampul album musik
134. PosterPrompt.tsx         - Prompt desain poster
135. MemeTemplateIdea.tsx     - Ide template meme
136. QRCodeIdeas.tsx          - Ide desain QR code artistik
137. EmojiSetPrompt.tsx       - Prompt untuk set emoji custom
138. AvatarPrompt.tsx         - Prompt untuk avatar/profile picture
139. NFTArtPrompt.tsx         - Prompt untuk NFT art

### ══════════════════════════════════
### KATEGORI 4: 🔊 TOOLS AUDIO (28 tools)
### ══════════════════════════════════
# File: src/tools/audio/

140. TextToSpeech.tsx         - Konversi teks ke suara
141. SpeechToText.tsx         - Transkripsi audio ke teks
142. AudioTranslator.tsx      - Transkripsi + terjemah audio
143. PodcastTranscriber.tsx   - Transkripsi episode podcast
144. MeetingTranscriber.tsx   - Transkripsi rekaman meeting
145. LectureTranscriber.tsx   - Transkripsi kuliah/seminar
146. SpeechSummarizer.tsx     - Ringkas isi audio/podcast
147. VoiceNoteToEmail.tsx     - Ubah voice note jadi email formal
148. VoiceNoteToTask.tsx      - Ekstrak tugas dari voice note
149. InterviewTranscriber.tsx - Transkripsi wawancara
150. AudioPrompter.tsx        - Buat skrip untuk rekaman suara
151. VoiceoverScript.tsx      - Skrip untuk voice over video
152. AudiobookScript.tsx      - Buat skrip audiobook dari teks
153. RadioScriptWriter.tsx    - Skrip iklan radio
154. SongLyricsAnalyzer.tsx   - Analisis makna lirik lagu
155. MusicPromptGenerator.tsx - Prompt untuk AI music generator (Suno/Udio)
156. SoundEffectPrompt.tsx    - Prompt untuk sound effect
157. PodcastIntroScript.tsx   - Buat skrip intro podcast
158. JingleWriter.tsx         - Buat lirik jingle iklan
159. ASMRScriptWriter.tsx     - Skrip konten ASMR
160. AudioDescriptionWriter.tsx- Buat deskripsi audio untuk video
161. SpeechCoachFeedback.tsx  - Feedback naskah pidato
162. PresentationScript.tsx   - Skrip presentasi
163. SpeechDebateArgument.tsx - Argumen untuk debat/pidato
164. DubScript.tsx            - Buat skrip dubbing
165. SubtitleWriter.tsx       - Buat subtitle dari transkripsi
166. SRTFormatter.tsx         - Format transkripsi ke .SRT subtitle
167. AudioTrimPrompt.tsx      - Rekomendasi kapan harus trim audio

### ══════════════════════════════════
### KATEGORI 5: 🎥 TOOLS VIDEO (22 tools)
### ══════════════════════════════════
# File: src/tools/video/

168. VideoScriptWriter.tsx    - Skrip video lengkap dengan scene
169. VideoOutlineCreator.tsx  - Outline video step-by-step
170. VideoHookWriter.tsx      - Hook 3-5 detik pertama video
171. VideoTransitionIdeas.tsx - Ide transisi antar scene
172. BRollIdeas.tsx           - Ide footage B-roll untuk video
173. VideoTitleABTest.tsx     - A/B test judul video
174. VideoEndScreenScript.tsx - Skrip end screen/outro
175. ViralAnalyzerYoutube.tsx - Analisis potensi viral YouTube
176. ShortsScriptWriter.tsx   - Skrip YouTube Shorts/Reels
177. VideoAdScript.tsx        - Skrip iklan video (30/60 detik)
178. EducationalVideoScript.tsx- Skrip video edukasi
179. DocumentaryScript.tsx    - Skrip dokumenter pendek
180. StoryboardTextCreator.tsx- Buat storyboard teks per scene
181. VideoDescriptionWriter.tsx- Deskripsi video YouTube SEO
182. VideoChapterMarkers.tsx  - Buat chapter markers YouTube
183. VideoCallToAction.tsx    - CTA untuk akhir video
184. VideoCritique.tsx        - Kritik/feedback skrip video
185. WatchTimeOptimizer.tsx   - Tips optimasi watch time
186. ThumbnailABTest.tsx      - A/B test konsep thumbnail
187. VideoSeriesPlanner.tsx   - Rencanakan seri video
188. ShortFormStrategy.tsx    - Strategi konten short-form
189. VideoRepurposer.tsx      - Ubah video panjang jadi multi-format

### ══════════════════════════════════
### KATEGORI 6: 💻 TOOLS DEVELOPER (62 tools)
### ══════════════════════════════════
# File: src/tools/developer/
# Catatan: Mix antara AI tools dan tools lokal (non-AI)

190. CodeExplainer.tsx        - Jelaskan kode yang membingungkan (AI)
191. CodeReviewer.tsx         - Review kode + saran perbaikan (AI)
192. CodeDebugger.tsx         - Debug error + solusi (AI)
193. CodeConverter.tsx        - Konversi kode antar bahasa (AI)
194. CodeOptimizer.tsx        - Optimasi performa kode (AI)
195. CodeDocGenerator.tsx     - Buat dokumentasi kode (AI)
196. CodeCommentWriter.tsx    - Tambahkan komentar ke kode (AI)
197. RegexGenerator.tsx       - Generate regex dari deskripsi (AI)
198. SQLQueryWriter.tsx       - Buat query SQL dari bahasa alami (AI)
199. SQLOptimizer.tsx         - Optimasi query SQL (AI)
200. APIDocWriter.tsx         - Buat dokumentasi API (AI)
201. READMEWriter.tsx         - Buat README.md project (AI)
202. GitCommitMessage.tsx     - Buat pesan commit Git yang baik (AI)
203. GitIgnoreGenerator.tsx   - Buat .gitignore untuk tech stack (AI)
204. DockerfileGenerator.tsx  - Buat Dockerfile (AI)
205. CICDPipelineWriter.tsx   - Buat config CI/CD (AI)
206. EnvFileGenerator.tsx     - Template .env file (AI)
207. UnitTestWriter.tsx       - Buat unit test dari kode (AI)
208. MockDataGenerator.tsx    - Generate mock/dummy data JSON (LOCAL)
209. JSONFormatter.tsx        - Format + validasi JSON (LOCAL)
210. JSONtoCSV.tsx            - Konversi JSON ke CSV (LOCAL)
211. CSVtoJSON.tsx            - Konversi CSV ke JSON (LOCAL)
212. XMLFormatter.tsx         - Format + validasi XML (LOCAL)
213. MarkdownEditor.tsx       - Editor Markdown dengan preview (LOCAL)
214. HTMLGenerator.tsx        - Buat HTML dari deskripsi (AI)
215. CSSGenerator.tsx         - Buat CSS dari deskripsi desain (AI)
216. TailwindConverter.tsx    - Konversi CSS biasa ke Tailwind (AI)
217. JSFunctionWriter.tsx     - Buat fungsi JavaScript (AI)
218. PythonFunctionWriter.tsx - Buat fungsi Python (AI)
219. AlgorithmExplainer.tsx   - Jelaskan algoritma (AI)
220. DataStructureExplainer.tsx- Jelaskan struktur data (AI)
221. DesignPatternAdvisor.tsx - Rekomendasi design pattern (AI)
222. ArchitectureAdvisor.tsx  - Rekomendasi arsitektur sistem (AI)
223. SecurityChecker.tsx      - Cek kerentanan keamanan kode (AI)
224. PerformanceTips.tsx      - Tips optimasi performa web (AI)
225. AccessibilityChecker.tsx - Cek aksesibilitas UI dari deskripsi (AI)
226. SEOTechAudit.tsx         - Audit teknis SEO (AI)
227. PWAChecklist.tsx         - Checklist Progressive Web App (AI)
228. APIEndpointDesigner.tsx  - Desain endpoint API RESTful (AI)
229. DatabaseSchemaDesigner.tsx- Desain skema database (AI)
230. ERDiagramTextCreator.tsx - Buat ER diagram dalam teks (AI)
231. SystemDesignHelper.tsx   - Bantu desain sistem skala besar (AI)
232. TechStackAdvisor.tsx     - Rekomendasi tech stack untuk proyek (AI)
233. DependencyAnalyzer.tsx   - Analisis package.json (AI)
234. ErrorMessageExplainer.tsx- Jelaskan error message (AI)
235. LogAnalyzer.tsx          - Analisis log aplikasi (AI)
236. CodeSnippetLibrary.tsx   - Koleksi snippet code berguna (LOCAL)
237. TerminalCommandHelper.tsx- Buat perintah terminal/bash (AI)
238. LinuxCommandExplainer.tsx- Jelaskan perintah Linux (AI)
239. CronJobGenerator.tsx     - Buat ekspresi cron job (AI)
240. WebhookHelper.tsx        - Buat handler webhook (AI)
241. GraphQLHelper.tsx        - Buat query/mutation GraphQL (AI)
242. SocketIOHelper.tsx       - Kode Socket.io dasar (AI)
243. LocalStorageHelper.tsx   - Manajemen localStorage (LOCAL)
244. CookieManager.tsx        - Manajemen cookie (LOCAL)
245. ColorCodeConverter.tsx   - Konversi HEX/RGB/HSL (LOCAL)
246. Base64Tool.tsx           - Encode/decode Base64 (LOCAL)
247. HashGenerator.tsx        - Generate hash MD5/SHA (LOCAL)
248. URLEncoder.tsx           - Encode/decode URL (LOCAL)
249. JWTDecoder.tsx           - Decode JWT token (LOCAL)
250. TimestampConverter.tsx   - Konversi Unix timestamp (LOCAL)
251. UUIDGenerator.tsx        - Generate UUID (LOCAL)

### ══════════════════════════════════
### KATEGORI 7: 🔍 TOOLS SEO (42 tools)
### ══════════════════════════════════
# File: src/tools/seo/

252. KeywordResearch.tsx      - Riset keyword dari topik (AI)
253. KeywordCluster.tsx       - Kelompokkan keyword serupa (AI)
254. LongTailKeyword.tsx      - Temukan keyword long-tail (AI)
255. KeywordDifficulty.tsx    - Estimasi kesulitan keyword (AI)
256. SearchIntentAnalyzer.tsx - Analisis intent keyword (AI)
257. LSIKeywordGenerator.tsx  - Generator keyword LSI (AI)
258. KeywordGapAnalysis.tsx   - Analisis gap keyword vs kompetitor (AI)
259. TitleTagOptimizer.tsx    - Optimasi title tag halaman (AI)
260. MetaDescOptimizer.tsx    - Optimasi meta deskripsi (AI)
261. URLSlugGenerator.tsx     - Buat URL slug SEO-friendly (AI)
262. HeaderStructurePlanner.tsx- Rencana struktur H1/H2/H3 (AI)
263. ContentBriefWriter.tsx   - Buat content brief untuk penulis (AI)
264. SEOContentOutline.tsx    - Outline konten SEO (AI)
265. FeaturedSnippetOptimizer.tsx- Optimasi untuk featured snippet (AI)
266. SchemaMarkupGenerator.tsx- Buat schema markup JSON-LD (AI)
267. FAQSchemaWriter.tsx      - Buat FAQ schema markup (AI)
268. BreadcrumbSchema.tsx     - Buat breadcrumb schema (AI)
269. LocalSEOOptimizer.tsx    - Optimasi SEO lokal (AI)
270. GBPDescWriter.tsx        - Deskripsi Google Business Profile (AI)
271. BacklinkOutreachEmail.tsx - Email outreach backlink (AI)
272. GuestPostPitch.tsx       - Pitch artikel tamu (AI)
273. InternalLinkingStrategy.tsx- Strategi internal linking (AI)
274. AnchorTextGenerator.tsx  - Generator anchor text natural (AI)
275. CompetitorContentGap.tsx - Analisis gap konten vs kompetitor (AI)
276. TopicClusterPlanner.tsx  - Rencanakan topic cluster (AI)
277. PillarPageOutline.tsx    - Outline halaman pilar (AI)
278. ContentAuditHelper.tsx   - Panduan audit konten lama (AI)
279. RedirectMapper.tsx       - Rencana redirect 301 (AI)
280. SitemapPlanner.tsx       - Rencana struktur sitemap (AI)
281. RobotstxtGenerator.tsx   - Buat robots.txt (AI)
282. HreflangHelper.tsx       - Buat tag hreflang (AI)
283. PageSpeedTips.tsx        - Tips optimasi PageSpeed (AI)
284. CoreWebVitals.tsx        - Penjelasan dan tips Core Web Vitals (AI)
285. EEATChecker.tsx          - Audit E-E-A-T konten (AI)
286. SEOAuditChecklist.tsx    - Checklist audit SEO lengkap (AI)
287. LocalCitationTemplate.tsx- Template NAP citations (AI)
288. GoogleAdsKeyword.tsx     - Riset keyword Google Ads (AI)
289. AdCopyWriter.tsx         - Buat teks iklan Google/Meta Ads (AI)
290. ABTestHeadline.tsx       - A/B test headline iklan (AI)
291. BacklinkChecker.tsx      - Analisis backlink kompetitor (AI)
292. DomainAuthorityTips.tsx  - Tips meningkatkan domain authority (AI)
293. RankingFactorsGuide.tsx  - Panduan faktor ranking Google (AI)

---

---

## 📝 CATATAN PENTING

✅ **Project Info:**
- Nama: **Gondrong Tools**
- Creator: **MaddazXD - Gondrong STIES**
- Built on: **Puter.js Platform** (gratis, tanpa API key)
- Total Tools: **850+** (600+ AI + 250+ Local)

✅ **AI Models yang Tersedia:**
1. **Claude Sonnet 4.6** - Cepat & efisien (default)
2. **Claude Opus 4.7** - Powerful & akurat

✅ **Fitur Utama:**
- 600+ AI-powered tools
- 250+ offline/local tools
- Real-time model selection
- Favorites & recent history
- Search functionality
- Organized by 15+ categories

✅ **Technology Stack:**
- React 18 + TypeScript
- Vite (lightning-fast bundler)
- TailwindCSS (modern styling)
- Zustand (state management)
- Puter.js (AI + File System + Auth)
- Lucide Icons (beautiful icons)

✅ **Status:**
- ✨ Fully functional blueprint ready for deployment
- 🎨 Modern, responsive UI with dark theme
- 🚀 Production-ready code structure
- 📦 All dependencies listed in package.json
