# ╔══════════════════════════════════════════════════════════════════════════╗
# ║   PUTERTOOLS V2 - MEGA PLATFORM: AI + NON-AI TOOLS                      ║
# ║   Prompt untuk Replit AI Agent                                           ║
# ║   AI Models: claude-opus-4-6 & claude-sonnet-4-6 (pilihan user)          ║
# ║   Platform: Puter.js (gratis, tanpa API key)                             ║
# ║   Stack: React + TypeScript + Vite + TailwindCSS                         ║
# ╚══════════════════════════════════════════════════════════════════════════╝

---

## 🚨 INSTRUKSI UTAMA UNTUK REPLIT AI AGENT

Kamu adalah senior full-stack developer. Tugasmu adalah membangun **PuterTools V2** — sebuah website platform tools raksasa dengan **600+ AI Tools** dan **250+ Non-AI Tools** yang bisa langsung dipakai di browser.

**WAJIB DIBACA SEBELUM MULAI:**
1. Baca SEMUA instruksi ini sampai selesai
2. Buat SEMUA file secara paralel — jangan skip satu pun
3. Setiap file harus FULLY FUNCTIONAL — tidak ada placeholder, tidak ada TODO
4. User bisa MEMILIH model AI: `claude-opus-4-6` atau `claude-sonnet-4-6`
5. Tools Non-AI harus berjalan 100% offline (tanpa Puter, tanpa API)
6. Footer WAJIB ada link "Powered by Puter" → https://developer.puter.com

---

## 📦 SETUP PROYEK

### package.json
```json
{
  "name": "putertools-v2",
  "version": "2.0.0",
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
  <title>PuterTools V2 — 850+ Tools Gratis</title>
  <meta name="description" content="Platform 850+ tools gratis: AI dengan Puter.js + 250+ tools non-AI offline. Pilih model AI sesukamu!">
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
putertools-v2/
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
    │   └── toolRegistry.ts     ← Daftar semua 850+ tools
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
    │       ├── ModelSelector.tsx ← BARU: pilih claude-opus-4-6 atau claude-sonnet-4-6
    │       ├── ToolBadge.tsx    ← Badge "AI" atau "Local"
    │       └── SearchBar.tsx
    │
    ├── pages/
    │   ├── HomePage.tsx         ← Halaman utama dengan grid semua tools
    │   ├── CategoryPage.tsx     ← Halaman per kategori
    │   └── ToolPage.tsx         ← Wrapper render tool aktif
    │
    ├── tools/
    │   ├── writing/             ← 52 tools AI
    │   ├── content/             ← 55 tools AI
    │   ├── image/               ← 32 tools AI
    │   ├── audio/               ← 28 tools AI
    │   ├── video/               ← 22 tools AI
    │   ├── developer/           ← 62 tools (mix AI + lokal)
    │   ├── seo/                 ← 42 tools AI
    │   ├── social/              ← 48 tools AI
    │   ├── productivity/        ← 50 tools (mix AI + lokal)
    │   ├── education/           ← 40 tools AI
    │   ├── business/            ← 42 tools (mix AI + lokal)
    │   ├── data/                ← 30 tools (mix AI + lokal)
    │   ├── health/              ← 20 tools AI
    │   ├── legal/               ← 20 tools AI
    │   ├── finance/             ← 22 tools (mix AI + lokal)
    │   ├── fun/                 ← 25 tools AI
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

---

### src/store/useAppStore.ts — ZUSTAND STORE (Model Selector WAJIB)
```typescript
import { create } from "zustand";
import { persist } from "zustand/middleware";

export type AIModel = "claude-opus-4-6" | "claude-sonnet-4-6";

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

      // Default model: claude-sonnet-4-6 (lebih cepat)
      selectedModel: "claude-sonnet-4-6",
      setSelectedModel: (model) => set({ selectedModel: model }),

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
    { name: "putertools-v2-store" }
  )
);
```

---

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

---

### src/components/UI/ModelSelector.tsx — KOMPONEN WAJIB
```tsx
import { useAppStore, AIModel } from "../../store/useAppStore";

const MODELS: { value: AIModel; label: string; desc: string; badge: string }[] = [
  {
    value: "claude-sonnet-4-6",
    label: "Claude Sonnet 4.6",
    desc: "Cepat & efisien — cocok untuk sehari-hari",
    badge: "⚡ Cepat",
  },
  {
    value: "claude-opus-4-6",
    label: "Claude Opus 4.6",
    desc: "Paling cerdas — cocok untuk tugas kompleks",
    badge: "🧠 Terkuat",
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
                ? "bg-violet-600 text-white shadow-lg shadow-violet-900/50"
                : "text-gray-400 hover:text-white hover:bg-gray-700"
            }`}
          >
            {m.badge} {m.value === "claude-opus-4-6" ? "Opus" : "Sonnet"}
          </button>
        ))}
      </div>
    </div>
  );
}
```

---

## 🤖 TEMPLATE TOOL AI (Wajib untuk semua tools AI)

Setiap tool AI harus menggunakan template ini PERSIS — termasuk `useAppStore` untuk model:

```tsx
// src/tools/[kategori]/NamaTool.tsx
import { useState } from "react";
import { useAppStore } from "../../store/useAppStore";
import Card from "../../components/UI/Card";
import Button from "../../components/UI/Button";
import Textarea from "../../components/UI/Textarea";
import StreamOutput from "../../components/UI/StreamOutput";
import CopyButton from "../../components/UI/CopyButton";
import Spinner from "../../components/UI/Spinner";
import ToolBadge from "../../components/UI/ToolBadge";

const TOOL_NAME = "Nama Tool";
const TOOL_DESC = "Deskripsi singkat apa yang tool ini lakukan";
const DISCLAIMER = ""; // isi jika perlu (kesehatan/hukum/keuangan)

export default function NamaTool() {
  const { selectedModel } = useAppStore();
  const [input, setInput] = useState("");
  const [output, setOutput] = useState("");
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");
  const [streaming, setStreaming] = useState(false);

  const handleGenerate = async () => {
    if (!input.trim()) return setError("Input tidak boleh kosong.");
    setLoading(true);
    setError("");
    setOutput("");
    setStreaming(true);

    try {
      const prompt = `[PROMPT SPESIFIK TOOL - Bahasa Indonesia]
Input: ${input}
Berikan output terstruktur, berguna, dan langsung to the point dalam Bahasa Indonesia.`;

      const stream = await window.puter.ai.chat(prompt, {
        model: selectedModel,   // ← SELALU pakai selectedModel dari store
        stream: true,
      });

      let fullText = "";
      for await (const chunk of stream) {
        fullText += chunk?.text ?? "";
        setOutput(fullText);
      }
    } catch (err: unknown) {
      setError("Error: " + (err instanceof Error ? err.message : String(err)));
    } finally {
      setLoading(false);
      setStreaming(false);
    }
  };

  return (
    <div className="max-w-3xl mx-auto space-y-4">
      <div className="flex items-start justify-between">
        <div>
          <h2 className="text-2xl font-bold text-white">{TOOL_NAME}</h2>
          <p className="text-gray-400 mt-1 text-sm">{TOOL_DESC}</p>
          {DISCLAIMER && (
            <p className="text-yellow-400 text-xs mt-2 p-2 bg-yellow-500/10 rounded-lg border border-yellow-500/20">
              ⚠️ {DISCLAIMER}
            </p>
          )}
        </div>
        <ToolBadge type="ai" model={selectedModel} />
      </div>

      <Card>
        <Textarea
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="Masukkan input di sini..."
          rows={4}
          disabled={loading}
        />
        {error && <p className="text-red-400 text-sm mt-2">{error}</p>}
        <Button onClick={handleGenerate} disabled={loading || !input.trim()} className="mt-3 w-full">
          {loading ? <Spinner /> : "✨ Generate"}
        </Button>
      </Card>

      {output && (
        <Card>
          <div className="flex justify-between items-center mb-2">
            <span className="text-gray-400 text-xs">Hasil ({selectedModel}):</span>
            <CopyButton text={output} />
          </div>
          <StreamOutput text={output} streaming={streaming} />
        </Card>
      )}
    </div>
  );
}
```

---

## 🔧 TEMPLATE TOOL NON-AI (Untuk semua 250+ tools lokal)

Tools non-AI harus 100% berjalan offline — tidak memanggil window.puter.ai sama sekali:

```tsx
// src/tools/local/[subfolder]/NamaToolLokal.tsx
import { useState } from "react";
import Card from "../../../components/UI/Card";
import Button from "../../../components/UI/Button";
import Input from "../../../components/UI/Input";
import CopyButton from "../../../components/UI/CopyButton";
import ToolBadge from "../../../components/UI/ToolBadge";

const TOOL_NAME = "Nama Tool Lokal";
const TOOL_DESC = "Deskripsi — berjalan 100% offline di browser";

export default function NamaToolLokal() {
  const [input, setInput] = useState("");
  const [output, setOutput] = useState("");
  const [error, setError] = useState("");

  const handleProcess = () => {
    if (!input.trim()) return setError("Input tidak boleh kosong.");
    setError("");

    try {
      // LOGIKA TOOL — Semua JavaScript murni, tidak ada API call
      const result = /* ... implementasi ... */ input.toUpperCase();
      setOutput(result);
    } catch (err) {
      setError("Error: " + String(err));
    }
  };

  return (
    <div className="max-w-3xl mx-auto space-y-4">
      <div className="flex items-start justify-between">
        <div>
          <h2 className="text-2xl font-bold text-white">{TOOL_NAME}</h2>
          <p className="text-gray-400 mt-1 text-sm">{TOOL_DESC}</p>
        </div>
        <ToolBadge type="local" />
      </div>

      <Card>
        <Input
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="Masukkan input..."
        />
        {error && <p className="text-red-400 text-sm mt-2">{error}</p>}
        <Button onClick={handleProcess} disabled={!input.trim()} className="mt-3 w-full">
          🔧 Proses
        </Button>
      </Card>

      {output && (
        <Card>
          <div className="flex justify-between items-center mb-2">
            <span className="text-gray-400 text-xs">Hasil (Offline):</span>
            <CopyButton text={output} />
          </div>
          <pre className="text-green-400 text-sm font-mono whitespace-pre-wrap break-words bg-gray-900 p-3 rounded-lg">
            {output}
          </pre>
        </Card>
      )}
    </div>
  );
}
```

---

## 🆕 DAFTAR LENGKAP 250+ TOOLS NON-AI (KATEGORI BARU)

### ══════════════════════════════════
### 📝 LOCAL/TEXT — 50 Tools Manipulasi Teks Offline
### ══════════════════════════════════
# File: src/tools/local/text/

001. WordCounter.tsx              - Hitung kata, karakter, kalimat, paragraf secara real-time
002. CharacterCounter.tsx         - Counter karakter dengan batas maksimum (Twitter, SMS, dll)
003. TextReverser.tsx             - Balik urutan teks / per kata / per kalimat
004. TextSorter.tsx               - Urutkan baris teks (A-Z, Z-A, random, panjang)
005. DuplicateLineRemover.tsx     - Hapus baris duplikat dari teks
006. EmptyLineRemover.tsx         - Hapus baris kosong dari teks
007. LineNumberAdder.tsx          - Tambah nomor baris ke setiap baris teks
008. TextCaseConverter.tsx        - Ubah case: UPPER, lower, Title, camelCase, snake_case, PascalCase, kebab-case, SCREAMING_SNAKE
009. WhitespaceRemover.tsx        - Hapus spasi berlebih, tab, whitespace
010. TextTrimmer.tsx              - Trim kiri, kanan, atau kedua sisi setiap baris
011. FindAndReplace.tsx           - Cari dan ganti teks (support regex)
012. TextDiff.tsx                 - Bandingkan dua teks, tampilkan perbedaan
013. TextMerger.tsx               - Gabungkan banyak blok teks dengan separator
014. TextSplitter.tsx             - Pecah teks berdasarkan karakter/kata/kalimat/paragraf
015. TextExtractor.tsx            - Ekstrak email, URL, nomor telepon, angka dari teks
016. TextRandomizer.tsx           - Acak urutan baris teks
017. TextRepeat.tsx               - Ulangi teks N kali
018. PalindromeChecker.tsx        - Cek apakah kata/kalimat adalah palindrom
019. AnagramChecker.tsx           - Cek apakah dua kata adalah anagram
020. VowelConsonantCounter.tsx    - Hitung vokal dan konsonan
021. SentenceLengthAnalyzer.tsx   - Analisis panjang setiap kalimat
022. ReadingTimeEstimator.tsx     - Estimasi waktu baca teks (WPM)
023. UniqueWordCounter.tsx        - Hitung kata unik dan frekuensinya
024. MostFrequentWords.tsx        - Tampilkan N kata paling sering muncul
025. TextToList.tsx               - Ubah teks paragraf jadi list berpoin
026. ListToText.tsx               - Gabung list jadi teks paragraf
027. CSVtoTable.tsx               - Render CSV sebagai tabel HTML visual
028. TextSlug.tsx                 - Ubah judul/teks jadi URL slug (lowercase, tanpa spasi)
029. TextCleaner.tsx              - Bersihkan teks dari karakter spesial/HTML entities
030. HTMLEntityEncoder.tsx        - Encode/decode HTML entities (&amp;, &lt;, dll)
031. TextTruncator.tsx            - Potong teks pada N karakter/kata dengan ellipsis
032. ColumnExtractor.tsx          - Ekstrak kolom tertentu dari teks terstruktur/CSV
033. LineJoiner.tsx               - Gabung semua baris jadi satu baris
034. AddPrefix.tsx                - Tambah prefix ke setiap baris teks
035. AddSuffix.tsx                - Tambah suffix ke setiap baris teks
036. TextStripper.tsx             - Hapus semua HTML tags dari teks
037. PunctuationRemover.tsx       - Hapus semua tanda baca dari teks
038. DigitExtractor.tsx           - Ekstrak semua angka dari teks
039. LetterExtractor.tsx          - Ekstrak hanya huruf dari teks
040. SpecialCharRemover.tsx       - Hapus karakter non-ASCII / spesial
041. AsciiArtGenerator.tsx        - Buat ASCII art dari teks (figlet-style)
042. TextToMorse.tsx              - Konversi teks ke kode Morse (dan sebaliknya)
043. TextToBinary.tsx             - Konversi teks ke biner (0s dan 1s) dan sebaliknya
044. TextToHex.tsx                - Konversi teks ke hex dan sebaliknya
045. TextToAscii.tsx              - Tampilkan nilai ASCII setiap karakter
046. SpaceToTab.tsx               - Konversi spasi ke tab dan sebaliknya
047. TextPadder.tsx               - Pad teks ke kiri/kanan/tengah dengan karakter pilihan
048. StringInterpolator.tsx       - Template string sederhana: ganti {variabel} dengan nilai
049. TextStatistics.tsx           - Statistik lengkap teks: Flesch score, avg sentence, dll
050. LoremIpsumGenerator.tsx      - Generate Lorem Ipsum dalam berbagai panjang

### ══════════════════════════════════
### 🔄 LOCAL/CONVERTER — 60 Tools Konverter Offline
### ══════════════════════════════════
# File: src/tools/local/converter/

051. JSONFormatter.tsx            - Format/minify/validasi JSON dengan syntax highlighting
052. JSONtoCSV.tsx                - Konversi array JSON ke format CSV
053. CSVtoJSON.tsx                - Konversi CSV ke format JSON
054. JSONtoYAML.tsx               - Konversi JSON ke YAML
055. YAMLtoJSON.tsx               - Konversi YAML ke JSON
056. JSONtoXML.tsx                - Konversi JSON ke XML
057. XMLtoJSON.tsx                - Konversi XML ke JSON sederhana
058. XMLFormatter.tsx             - Format/minify/validasi XML
059. MarkdownToHTML.tsx           - Konversi Markdown ke HTML (parser lokal)
060. HTMLToMarkdown.tsx           - Konversi HTML ke Markdown
061. CSVtoHTML.tsx                - Konversi CSV ke tabel HTML
062. JSONtoTable.tsx              - Render JSON array sebagai tabel HTML interaktif
063. Base64Encoder.tsx            - Encode teks/file ke Base64
064. Base64Decoder.tsx            - Decode Base64 ke teks/file
065. URLEncoder.tsx               - Encode/decode URL (encodeURIComponent)
066. URLParser.tsx                - Parsing URL: protocol, host, path, params, hash
067. QueryStringBuilder.tsx       - Build dan parse query string URL
068. JWTDecoder.tsx               - Decode payload JWT token (tanpa verifikasi)
069. Base32Encoder.tsx            - Encode/decode Base32
070. HexToRGB.tsx                 - Konversi warna: HEX ↔ RGB ↔ HSL ↔ HSV
071. ColorConverter.tsx           - Konverter warna lengkap: HEX, RGB, HSL, HSV, CMYK, CSS
072. NumberBaseConverter.tsx      - Konversi bilangan: Desimal ↔ Biner ↔ Oktal ↔ Hex
073. RomanNumeralConverter.tsx    - Konversi angka Arab ↔ Angka Romawi
074. TemperatureConverter.tsx     - Celsius ↔ Fahrenheit ↔ Kelvin ↔ Rankine
075. LengthConverter.tsx          - Konversi satuan panjang: cm, m, km, inch, ft, mile, dll
076. WeightConverter.tsx          - Konversi satuan berat: kg, g, lb, oz, stone, dll
077. VolumeConverter.tsx          - Konversi satuan volume: ml, L, gallon, pint, cup, dll
078. AreaConverter.tsx            - Konversi satuan luas: m², km², ft², acre, hectare, dll
079. SpeedConverter.tsx           - Konversi kecepatan: km/h, m/s, mph, knot, dll
080. DataSizeConverter.tsx        - Konversi ukuran data: bit, byte, KB, MB, GB, TB, PB
081. TimeZoneConverter.tsx        - Konversi waktu antar timezone dunia
082. UnixTimestampConverter.tsx   - Konversi Unix timestamp ↔ tanggal manusia
083. DateFormatConverter.tsx      - Konversi format tanggal: DD/MM/YYYY ↔ YYYY-MM-DD ↔ dll
084. DurationConverter.tsx        - Konversi durasi: detik ↔ menit ↔ jam ↔ hari
085. CurrencyFormatter.tsx        - Format angka sebagai mata uang berbagai negara (offline)
086. NumberFormatter.tsx          - Format angka: ribuan, desimal, ilmiah, persen
087. FractionConverter.tsx        - Konversi desimal ↔ pecahan (0.5 → 1/2)
088. AngleConverter.tsx           - Konversi sudut: derajat ↔ radian ↔ gradian
089. PressureConverter.tsx        - Konversi tekanan: Pa, bar, psi, atm, dll
090. EnergyConverter.tsx          - Konversi energi: Joule, kWh, kalori, BTU, dll
091. PowerConverter.tsx           - Konversi daya: Watt, kW, HP, dll
092. StorageConverter.tsx         - Konversi penyimpanan file dengan breakdown lengkap
093. PixelRemConverter.tsx        - Konversi px ↔ rem ↔ em ↔ pt ↔ vw/vh (CSS)
094. ImageResolutionCalc.tsx      - Hitung resolusi: PPI, DPI untuk ukuran cetak
095. AspectRatioCalc.tsx          - Hitung dan konversi aspect ratio (16:9, 4:3, dll)
096. CSStoSCSS.tsx               - Konversi CSS biasa ke format SCSS sederhana
097. HEXtoRGBA.tsx               - HEX + alpha → rgba() CSS
098. GradientsConverter.tsx       - Konversi gradient CSS antar format
099. SoundUnitConverter.tsx       - Konversi satuan suara: dB, amplitude, dll
100. FuelEconomyConverter.tsx     - Konversi konsumsi BBM: L/100km ↔ MPG ↔ km/L
101. CookingConverter.tsx         - Konversi satuan memasak: cup, tbsp, tsp, ml, gram
102. NutritionConverter.tsx       - Konversi unit nutrisi: kkal, kJ, IU, mcg
103. ResolutionConverter.tsx      - Konversi resolusi layar dan pixel density
104. FrequencyConverter.tsx       - Konversi frekuensi: Hz, kHz, MHz, GHz
105. VoltageConverter.tsx         - Konversi tegangan listrik dan daya
106. ResistanceConverter.tsx      - Konversi hambatan: Ohm, kΩ, MΩ
107. MagneticConverter.tsx        - Konversi satuan magnet: Tesla, Gauss
108. PrintSizeCalculator.tsx      - Hitung ukuran cetak dari pixel + DPI
109. ColorsNameFinder.tsx         - Temukan nama warna dari kode HEX
110. PantoneToHex.tsx             - Referensi konversi warna Pantone ↔ HEX

### ══════════════════════════════════
### ⚡ LOCAL/GENERATOR — 40 Tools Generator Offline
### ══════════════════════════════════
# File: src/tools/local/generator/

111. PasswordGenerator.tsx        - Generate password kuat dengan aturan kustom
112. PINGenerator.tsx             - Generate PIN numerik dengan panjang pilihan
113. UUIDGenerator.tsx            - Generate UUID v1/v4 dalam jumlah banyak
114. NanoIDGenerator.tsx          - Generate NanoID dengan alphabet dan panjang kustom
115. RandomStringGenerator.tsx    - Generate string acak: huruf, angka, simbol
116. RandomNumberGenerator.tsx    - Generate angka acak dalam rentang dengan distribusi
117. HashGenerator.tsx            - Hitung hash: MD5, SHA-1, SHA-256, SHA-512 (Web Crypto)
118. HMACGenerator.tsx            - Generate HMAC-SHA256 dari key + message
119. ChecksumCalculator.tsx       - Hitung checksum CRC32, Adler32
120. QRCodeGenerator.tsx          - Generate QR Code dari teks/URL (library qrcode.js CDN)
121. BarcodeGenerator.tsx         - Generate barcode: EAN-13, Code128, QR (CDN)
122. FaviconGenerator.tsx         - Generate favicon SVG sederhana dari teks/emoji
123. AvatarGenerator.tsx          - Generate avatar placeholder berdasarkan nama (canvas)
124. GravatarURL.tsx              - Generate URL Gravatar dari email (hash MD5)
125. PlaceholderImageURL.tsx      - Generate URL placeholder image (via.placeholder.com)
126. ColorPaletteGenerator.tsx    - Generate palet warna harmonis dari satu warna dasar
127. GradientGenerator.tsx        - Generator gradient CSS dengan preview langsung
128. ShadowGenerator.tsx          - Generator box-shadow CSS dengan preview
129. BorderRadiusGenerator.tsx    - Generator border-radius CSS visual
130. FontScaleGenerator.tsx       - Generate skala tipografi (major third, golden ratio, dll)
131. LineHeightCalc.tsx           - Hitung line-height optimal dari font size
132. GridSystemGenerator.tsx      - Generate grid CSS custom (columns, gap, dll)
133. FlexboxGenerator.tsx         - Visual builder flexbox CSS
134. CSSAnimationGenerator.tsx    - Generator keyframe CSS animation
135. CSSSelectorGenerator.tsx     - Helper menulis CSS selector kompleks
136. FakeEmailGenerator.tsx       - Generate email palsu realistis (random name + domain)
137. FakeNameGenerator.tsx        - Generate nama palsu Indonesia/internasional
138. FakePhoneGenerator.tsx       - Generate nomor telepon Indonesia acak (format valid)
139. FakeAddressGenerator.tsx     - Generate alamat palsu Indonesia
140. MockJSONGenerator.tsx        - Generate JSON dummy dari schema sederhana
141. RegexGenerator.tsx           - Build regex dari deskripsi pattern visual
142. RegexTester.tsx              - Test regex dengan input dan lihat matches
143. CronExpressionGenerator.tsx  - Build ekspresi cron secara visual
144. CronExpressionExplainer.tsx  - Jelaskan cron expression dalam bahasa manusia
145. ColorSchemeGenerator.tsx     - Generate color scheme: monochromatic, complementary, triadic
146. SymbolLibrary.tsx            - Kumpulan simbol Unicode, emoji, arrows — copy dengan klik
147. EmojiPicker.tsx              - Emoji picker dengan kategori dan search
148. HTMLColorCodes.tsx           - Referensi semua named CSS colors dengan preview
149. DataURIGenerator.tsx         - Encode file/teks ke Data URI (base64 inline)
150. SVGPatternGenerator.tsx      - Generate pola SVG: dots, stripes, crosshatch, dll

### ══════════════════════════════════
### 🧮 LOCAL/CALCULATOR — 50 Tools Kalkulator Offline
### ══════════════════════════════════
# File: src/tools/local/calculator/

151. ScientificCalculator.tsx     - Kalkulator saintifik lengkap: sin/cos/tan, log, sqrt, exp
152. PercentageCalculator.tsx     - Hitung persentase: X% dari Y, X adalah berapa% dari Y
153. DiscountCalculator.tsx       - Hitung harga setelah diskon + berapa hemat
154. TaxCalculator.tsx            - Hitung pajak PPN/PPh dari harga
155. TipCalculator.tsx            - Hitung tip restoran dan bagi per orang
156. BMICalculator.tsx            - Hitung BMI + kategori (underweight/normal/obese)
157. BMRCalculator.tsx            - Hitung Basal Metabolic Rate (Harris-Benedict)
158. TDEECalculator.tsx           - Hitung Total Daily Energy Expenditure
159. IdealWeightCalculator.tsx    - Hitung berat badan ideal (berbagai formula)
160. BodyFatCalculator.tsx        - Estimasi body fat percentage dari pengukuran
161. CalorieCalculator.tsx        - Hitung kalori harian berdasarkan tujuan (defisit/surplus)
162. MacroCalculator.tsx          - Hitung kebutuhan protein, karbohidrat, lemak harian
163. WaterIntakeCalculator.tsx    - Hitung kebutuhan air harian (berdasarkan berat + aktivitas)
164. SleepCalculator.tsx          - Hitung waktu tidur optimal berdasarkan siklus 90 menit
165. AgeCalculator.tsx            - Hitung usia tepat dalam tahun, bulan, hari, jam
166. DateDifferenceCalc.tsx       - Hitung selisih antar dua tanggal
167. DaysUntilCalc.tsx            - Hitung hari hingga tanggal tertentu (ulang tahun, event)
168. LoanCalculator.tsx           - Kalkulator cicilan KPR/KTA: angsuran, total bayar, bunga
169. MortgageCalculator.tsx       - Kalkulator KPR detail dengan tabel amortisasi
170. CompoundInterestCalc.tsx     - Kalkulator bunga majemuk investasi
171. SimpleSavingsCalc.tsx        - Simulasi tabungan dengan bunga sederhana
172. RetirementCalculator.tsx     - Estimasi dana pensiun berdasarkan target
173. EmergencyFundCalc.tsx        - Hitung kebutuhan dana darurat (3-12 bulan)
174. InvestmentROICalc.tsx        - Hitung Return on Investment
175. NetWorthCalc.tsx             - Hitung kekayaan bersih: aset - liabilitas
176. BudgetSplitter.tsx           - Bagi anggaran berdasarkan aturan 50/30/20
177. SplitBillCalculator.tsx      - Bagi tagihan ke beberapa orang (+ tip, pajak)
178. CurrencyPctChange.tsx        - Hitung perubahan persentase harga/nilai
179. BreakevenCalculator.tsx      - Hitung titik impas bisnis
180. ProfitMarginCalc.tsx         - Hitung profit margin (gross, net, operating)
181. MarkupCalculator.tsx         - Hitung markup harga dari HPP
182. FrequencyCalc.tsx            - Kalkulator frekuensi & panjang gelombang fisika
183. OhmsLawCalculator.tsx        - Kalkulator hukum Ohm: V=IR
184. PowerCalculator.tsx          - Kalkulator daya listrik: P=VI
185. ElectricityBillCalc.tsx      - Estimasi tagihan listrik dari pemakaian watt
186. FuelCostCalculator.tsx       - Hitung biaya BBM perjalanan (jarak + konsumsi)
187. SpeedDistanceTimeCalc.tsx    - Kalkulator kecepatan/jarak/waktu
188. TravelTimeCalc.tsx           - Estimasi waktu perjalanan dari jarak + kecepatan
189. TypingSpeedCalc.tsx          - Hitung WPM dari jumlah kata + waktu ketik
190. ReadSpeedCalc.tsx            - Hitung kecepatan baca (WPM) dari teks + waktu
191. GradeCalculator.tsx          - Hitung nilai akhir dari beberapa komponen + bobot
192. GPACalculator.tsx            - Hitung GPA dari daftar mata kuliah + nilai + SKS
193. PaceCalculator.tsx           - Kalkulator pace lari: min/km dari jarak & waktu
194. CalorieBurnCalc.tsx          - Estimasi kalori terbakar per aktivitas olahraga
195. PregnancyDueDateCalc.tsx     - Hitung HPL dari HPHT (Hari Pertama Haid Terakhir)
196. OvulationCalc.tsx            - Estimasi masa subur dari siklus menstruasi
197. FibonacciGenerator.tsx       - Generate deret Fibonacci hingga N suku
198. PrimeChecker.tsx             - Cek apakah angka prima + faktorisasi prima
199. FactorialCalc.tsx            - Hitung faktorial dan kombinasi/permutasi
200. StatisticsCalculator.tsx     - Hitung: mean, median, modus, std dev, variance dari dataset

### ══════════════════════════════════
### 🎨 LOCAL/FORMATTER — 30 Tools Formatter & Prettifier Offline
### ══════════════════════════════════
# File: src/tools/local/formatter/

201. SQLFormatter.tsx             - Format/beautify SQL query dengan indentasi rapi
202. CSSFormatter.tsx             - Format/minify CSS
203. HTMLFormatter.tsx            - Format/minify/validasi HTML
204. JavaScriptFormatter.tsx      - Format/minify JavaScript (basic)
205. JSONDiffViewer.tsx           - Bandingkan dua JSON, tampilkan perbedaan
206. MarkdownPreview.tsx          - Editor Markdown + live preview HTML
207. HTMLPreview.tsx              - Tulis HTML, lihat preview langsung di iframe
208. CSSPreview.tsx               - Tulis CSS, lihat hasil live (dengan div contoh)
209. SVGEditor.tsx                - Editor SVG dengan preview langsung
210. RegexVisualizer.tsx          - Visualisasi matches regex di teks dengan highlight
211. JSONPathTester.tsx           - Test JSONPath expression di JSON object
212. XPathTester.tsx              - Test XPath sederhana di XML
213. CSSGradientPreview.tsx       - Preview gradient CSS langsung dari kode
214. BoxShadowPreview.tsx         - Preview box-shadow CSS dari kode
215. TextShadowPreview.tsx        - Preview text-shadow CSS dari kode
216. BorderPreview.tsx            - Preview border CSS (style, width, color, radius)
217. TransformPreview.tsx         - Preview CSS transform: rotate, scale, skew, translate
218. AnimationPreview.tsx         - Preview CSS animation/keyframes sederhana
219. FontPreview.tsx              - Preview teks dengan Google Font pilihan
220. ColorContrastChecker.tsx     - Cek kontras warna foreground vs background (WCAG)
221. AccessibilityColorHelper.tsx - Cek aksesibilitas kombinasi warna (AA/AAA)
222. GridVisualizer.tsx           - Visualisasikan CSS Grid dari kode grid-template
223. FlexboxVisualizer.tsx        - Visualisasikan layout flexbox dari kode flex
224. SpacingPreview.tsx           - Preview margin/padding dengan visual box model
225. EasingPreview.tsx            - Preview CSS easing function (curve visualization)
226. NumberFormat.tsx             - Preview berbagai format angka: comma, dot, space separator
227. DateFormatPreview.tsx        - Preview format tanggal dari berbagai pattern
228. CSSVariablesExtractor.tsx    - Ekstrak semua CSS variables (--var) dari kode
229. TailwindToCSS.tsx            - Konversi Tailwind class ke CSS properties lengkap
230. CSSSpecificityCalc.tsx       - Hitung specificity selector CSS (a, b, c)

### ══════════════════════════════════
### 🛠️ LOCAL/UTILITY — 30 Tools Utility & Developer Tools Offline
### ══════════════════════════════════
# File: src/tools/local/utility/

231. LocalStorageManager.tsx      - Lihat, edit, hapus localStorage & sessionStorage browser
232. CookieManager.tsx            - Lihat dan hapus cookies di browser saat ini
233. ColorPickerTool.tsx          - Color picker lengkap: pilih warna, salin semua format
234. ScreenResolutionInfo.tsx     - Info layar: resolusi, DPR, viewport, orientasi
235. UserAgentParser.tsx          - Parse User Agent: browser, OS, device type
236. IPAddressInfo.tsx            - Info IP lokal + format + validasi
237. MACAddressGenerator.tsx      - Generate MAC address acak + format
238. SubnetCalculator.tsx         - Kalkulator subnet IPv4: network, broadcast, host range
239. PortNumberReference.tsx      - Referensi port terkenal (HTTP=80, HTTPS=443, dll)
240. HTTPStatusCodes.tsx          - Referensi semua HTTP status code + deskripsi
241. MIMETypeReference.tsx        - Referensi MIME type berdasarkan ekstensi file
242. CharsetReference.tsx         - Referensi karakter set: UTF-8, ASCII, Latin-1
243. KeycodeViewer.tsx            - Tampilkan keycode, key, dan code saat tekan tombol
244. ClipboardHistory.tsx         - Riwayat clipboard session (simpan di memory)
245. CountdownTimer.tsx           - Timer hitung mundur dengan suara alert
246. Stopwatch.tsx                - Stopwatch dengan lap time
247. WorldClock.tsx               - Jam digital multi-timezone (tidak perlu API)
248. MetronomeApp.tsx             - Metronom digital dengan BPM kustom (Web Audio API)
249. PomodoroClock.tsx            - Timer Pomodoro 25/5 dengan notifikasi
250. FlashcardApp.tsx             - Flashcard interaktif dengan KV store (simpan ke Puter)
251. NotepadApp.tsx               - Notepad sederhana dengan auto-save ke Puter KV
252. MarkdownNotes.tsx            - Catatan Markdown yang tersimpan di Puter KV
253. BookmarkManager.tsx          - Simpan bookmark/link di Puter KV
254. TaskListApp.tsx              - Todo list sederhana tersimpan di Puter KV
255. HabitTracker.tsx             - Tracker kebiasaan harian dengan visualisasi calendar
256. ExpenseTracker.tsx           - Tracker pengeluaran sederhana dengan kategori
257. BudgetApp.tsx                - Aplikasi budget bulanan sederhana (Puter KV)
258. PasswordManager.tsx          - Password manager lokal (tersimpan terenkripsi di Puter KV)
259. DiceRoller.tsx               - Dadu digital: d4, d6, d8, d10, d12, d20, custom
260. CoinFlipper.tsx              - Lempar koin dengan animasi dan statistik

---

## 📋 DAFTAR TOOLS AI (600+ tools — sama seperti blueprint asli)

Untuk daftar lengkap 600+ tools AI (Writing, Content, Image, Audio, Video, Developer, SEO, Social, Productivity, Education, Business, Data, Health, Legal, Finance, Fun), gunakan daftar dari blueprint asli dengan PERUBAHAN BERIKUT:

**PERUBAHAN WAJIB dari blueprint lama:**
1. Ganti `"claude-opus-4-7"` → gunakan `selectedModel` dari `useAppStore`
2. Tambahkan `<ToolBadge type="ai" model={selectedModel} />` di setiap tool AI
3. Tambahkan import `useAppStore` di setiap tool AI
4. Semua output harus menampilkan model yang digunakan: `"Hasil ({selectedModel})"`

---

## 🎨 DESAIN UI WAJIB

### Tema: Dark Mode Only
- Background utama: `bg-gray-950` (#030712)
- Card background: `bg-gray-900` (#111827)
- Border: `border-gray-800`
- Teks utama: `text-white`
- Teks sekunder: `text-gray-400`
- Aksen: `violet-500` / `violet-600`
- Success: `green-500`
- Error: `red-400`
- Warning: `yellow-400`
- Local badge: `bg-green-900/50 text-green-400 border border-green-700` — tampilkan "⚡ Offline"
- AI badge: `bg-violet-900/50 text-violet-400 border border-violet-700` — tampilkan "🤖 AI"

### Header (src/components/Layout/Header.tsx)
```
[Logo PuterTools V2] [Tagline: 850+ Tools Gratis]    [ModelSelector]    [Auth Button]
```
- ModelSelector WAJIB ada di header, selalu terlihat
- Warna aktif model: violet (pilihan aktif)

### Sidebar (src/components/Layout/Sidebar.tsx)
- Kategori bisa di-collapse/expand
- Badge jumlah tools per kategori
- Warna berbeda untuk tools AI (violet) vs Local (green)
- Kategori "🔧 Local Tools" harus ada sub-kategori: Text, Converter, Generator, Calculator, Formatter, Utility
- Sticky + scrollable
- Search bar di atas sidebar

### Footer (src/components/Layout/Footer.tsx)
```tsx
// WAJIB dari persyaratan Puter.js
<footer className="border-t border-gray-800 py-4 px-6 text-center">
  <a
    href="https://developer.puter.com"
    target="_blank"
    rel="noopener noreferrer"
    className="text-violet-400 hover:text-violet-300 text-sm transition-colors"
  >
    Powered by Puter
  </a>
  <span className="text-gray-600 text-sm mx-2">•</span>
  <span className="text-gray-600 text-sm">PuterTools V2 — 850+ Tools Gratis</span>
</footer>
```

### Halaman Utama (src/pages/HomePage.tsx)
```
[Hero Section: "850+ Tools Gratis — AI + Non-AI"]
[Subtext: "600+ AI Tools via Puter.js • 250+ Tools Offline • Pilih Model AI"]
[Search Bar Besar]
[Grid Kategori — 17 kategori (16 AI + 1 Local)]
[Featured Tools — 8 tools populer]
[Stats: X AI Tools • Y Local Tools • Z Total]
```

---

## 🔧 KOMPONEN UI WAJIB DETAIL

### ToolBadge.tsx
```tsx
type ToolBadgeProps = {
  type: "ai" | "local";
  model?: string;
};

export default function ToolBadge({ type, model }: ToolBadgeProps) {
  if (type === "local") {
    return (
      <span className="px-2 py-1 text-xs rounded-full bg-green-900/50 text-green-400 border border-green-700/50 font-medium">
        ⚡ Offline
      </span>
    );
  }
  return (
    <span className="px-2 py-1 text-xs rounded-full bg-violet-900/50 text-violet-400 border border-violet-700/50 font-medium">
      🤖 {model === "claude-opus-4-6" ? "Opus 4.6" : "Sonnet 4.6"}
    </span>
  );
}
```

### StreamOutput.tsx — Dengan auto-scroll
```tsx
import { useEffect, useRef } from "react";

type Props = { text: string; streaming?: boolean };

export default function StreamOutput({ text, streaming }: Props) {
  const ref = useRef<HTMLDivElement>(null);

  useEffect(() => {
    if (streaming && ref.current) {
      ref.current.scrollTop = ref.current.scrollHeight;
    }
  }, [text, streaming]);

  return (
    <div
      ref={ref}
      className="max-h-96 overflow-y-auto text-sm text-gray-200 font-mono whitespace-pre-wrap break-words bg-gray-950 p-4 rounded-lg border border-gray-800"
    >
      {text}
      {streaming && <span className="inline-block w-2 h-4 bg-violet-400 animate-pulse ml-0.5" />}
    </div>
  );
}
```

---

## 📊 TOOL REGISTRY (src/store/toolRegistry.ts)

Buat registry lengkap SEMUA tools (850+) dengan struktur:

```typescript
export type Tool = {
  id: string;
  label: string;
  description: string;
  category: string;
  type: "ai" | "local";
  tags?: string[];
  component: () => Promise<{ default: React.ComponentType }>;
};

export const ALL_TOOLS: Tool[] = [
  // ===== AI TOOLS =====
  {
    id: "article-writer",
    label: "Penulis Artikel",
    description: "Buat artikel blog panjang dari topik",
    category: "writing",
    type: "ai",
    tags: ["tulis", "blog", "konten"],
    component: () => import("../tools/writing/ArticleWriter"),
  },
  // ... semua 600+ AI tools

  // ===== LOCAL TOOLS =====
  {
    id: "word-counter",
    label: "Penghitung Kata",
    description: "Hitung kata, karakter, kalimat secara real-time",
    category: "local-text",
    type: "local",
    tags: ["kata", "teks", "counter", "offline"],
    component: () => import("../tools/local/text/WordCounter"),
  },
  // ... semua 260 local tools
];

export const CATEGORIES = [
  // 16 kategori AI ...
  {
    id: "local",
    icon: "🔧",
    label: "Local Tools",
    description: "250+ tools offline, tanpa AI, tanpa internet",
    badge: "⚡ Offline",
    color: "green",
    subCategories: [
      { id: "local-text", label: "Teks", icon: "📝", count: 50 },
      { id: "local-converter", label: "Konverter", icon: "🔄", count: 60 },
      { id: "local-generator", label: "Generator", icon: "⚡", count: 40 },
      { id: "local-calculator", label: "Kalkulator", icon: "🧮", count: 50 },
      { id: "local-formatter", label: "Formatter", icon: "🎨", count: 30 },
      { id: "local-utility", label: "Utility", icon: "🛠️", count: 30 },
    ],
  },
];
```

---

## 📝 CONTOH IMPLEMENTASI TOOLS LOCAL PENTING

### WordCounter.tsx — Real-time counter
```tsx
import { useState } from "react";
import Card from "../../../components/UI/Card";
import Textarea from "../../../components/UI/Textarea";
import ToolBadge from "../../../components/UI/ToolBadge";

export default function WordCounter() {
  const [text, setText] = useState("");

  const stats = {
    characters: text.length,
    charactersNoSpace: text.replace(/\s/g, "").length,
    words: text.trim() === "" ? 0 : text.trim().split(/\s+/).length,
    sentences: text === "" ? 0 : (text.match(/[.!?]+/g) || []).length,
    paragraphs: text === "" ? 0 : text.split(/\n\s*\n/).filter(Boolean).length,
    lines: text === "" ? 0 : text.split("\n").length,
    readingTime: Math.ceil(text.trim().split(/\s+/).filter(Boolean).length / 200),
    uniqueWords: new Set(text.toLowerCase().match(/\b\w+\b/g) || []).size,
  };

  return (
    <div className="max-w-3xl mx-auto space-y-4">
      <div className="flex items-start justify-between">
        <div>
          <h2 className="text-2xl font-bold text-white">Penghitung Kata</h2>
          <p className="text-gray-400 text-sm mt-1">Hitung kata, karakter, kalimat, paragraf secara real-time</p>
        </div>
        <ToolBadge type="local" />
      </div>

      <Textarea
        value={text}
        onChange={(e) => setText(e.target.value)}
        placeholder="Ketik atau paste teks di sini..."
        rows={8}
        className="w-full"
      />

      <div className="grid grid-cols-2 sm:grid-cols-4 gap-3">
        {[
          { label: "Kata", value: stats.words },
          { label: "Karakter", value: stats.characters },
          { label: "Tanpa Spasi", value: stats.charactersNoSpace },
          { label: "Kalimat", value: stats.sentences },
          { label: "Paragraf", value: stats.paragraphs },
          { label: "Baris", value: stats.lines },
          { label: "Kata Unik", value: stats.uniqueWords },
          { label: "Baca (mnt)", value: stats.readingTime },
        ].map((stat) => (
          <Card key={stat.label} className="text-center p-3">
            <div className="text-2xl font-bold text-violet-400">{stat.value.toLocaleString()}</div>
            <div className="text-gray-400 text-xs mt-1">{stat.label}</div>
          </Card>
        ))}
      </div>
    </div>
  );
}
```

### PasswordGenerator.tsx — Generator password kuat
```tsx
import { useState, useCallback } from "react";
import Card from "../../../components/UI/Card";
import Button from "../../../components/UI/Button";
import CopyButton from "../../../components/UI/CopyButton";
import ToolBadge from "../../../components/UI/ToolBadge";

const CHARSETS = {
  uppercase: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
  lowercase: "abcdefghijklmnopqrstuvwxyz",
  numbers: "0123456789",
  symbols: "!@#$%^&*()_+-=[]{}|;:,.<>?",
};

export default function PasswordGenerator() {
  const [length, setLength] = useState(16);
  const [options, setOptions] = useState({
    uppercase: true, lowercase: true, numbers: true, symbols: true,
  });
  const [count, setCount] = useState(5);
  const [passwords, setPasswords] = useState<string[]>([]);

  const generate = useCallback(() => {
    let charset = "";
    if (options.uppercase) charset += CHARSETS.uppercase;
    if (options.lowercase) charset += CHARSETS.lowercase;
    if (options.numbers) charset += CHARSETS.numbers;
    if (options.symbols) charset += CHARSETS.symbols;
    if (!charset) return;

    const newPasswords = Array.from({ length: count }, () =>
      Array.from(
        { length },
        () => charset[Math.floor(Math.random() * charset.length)]
      ).join("")
    );
    setPasswords(newPasswords);
  }, [length, options, count]);

  const getStrength = (len: number, optCount: number) => {
    const score = len * optCount;
    if (score < 32) return { label: "Lemah", color: "text-red-400" };
    if (score < 64) return { label: "Sedang", color: "text-yellow-400" };
    if (score < 96) return { label: "Kuat", color: "text-blue-400" };
    return { label: "Sangat Kuat", color: "text-green-400" };
  };

  const activeOptions = Object.values(options).filter(Boolean).length;
  const strength = getStrength(length, activeOptions);

  return (
    <div className="max-w-2xl mx-auto space-y-4">
      <div className="flex items-start justify-between">
        <div>
          <h2 className="text-2xl font-bold text-white">Generator Password</h2>
          <p className="text-gray-400 text-sm mt-1">Generate password kuat dengan aturan kustom — offline</p>
        </div>
        <ToolBadge type="local" />
      </div>

      <Card className="space-y-4">
        {/* Length slider */}
        <div>
          <div className="flex justify-between mb-1">
            <label className="text-gray-300 text-sm">Panjang: <span className="text-violet-400 font-bold">{length}</span></label>
            <span className={`text-sm font-medium ${strength.color}`}>{strength.label}</span>
          </div>
          <input
            type="range" min={6} max={128} value={length}
            onChange={(e) => setLength(Number(e.target.value))}
            className="w-full accent-violet-500"
          />
        </div>

        {/* Options */}
        <div className="grid grid-cols-2 gap-2">
          {(Object.keys(options) as (keyof typeof options)[]).map((key) => (
            <label key={key} className="flex items-center gap-2 cursor-pointer">
              <input
                type="checkbox"
                checked={options[key]}
                onChange={() => setOptions((prev) => ({ ...prev, [key]: !prev[key] }))}
                className="accent-violet-500 w-4 h-4"
              />
              <span className="text-gray-300 text-sm capitalize">
                {key === "uppercase" ? "HURUF BESAR" : key === "lowercase" ? "huruf kecil" : key === "numbers" ? "Angka 0-9" : "Simbol !@#$"}
              </span>
            </label>
          ))}
        </div>

        {/* Count */}
        <div className="flex items-center gap-3">
          <label className="text-gray-300 text-sm">Jumlah:</label>
          <input
            type="number" min={1} max={20} value={count}
            onChange={(e) => setCount(Math.min(20, Math.max(1, Number(e.target.value))))}
            className="w-20 bg-gray-800 text-white rounded px-2 py-1 text-sm border border-gray-700"
          />
        </div>

        <Button onClick={generate} className="w-full">🔐 Generate Password</Button>
      </Card>

      {passwords.length > 0 && (
        <Card className="space-y-2">
          {passwords.map((pw, i) => (
            <div key={i} className="flex items-center justify-between bg-gray-950 rounded p-2 gap-2">
              <code className="text-green-400 font-mono text-sm flex-1 break-all">{pw}</code>
              <CopyButton text={pw} />
            </div>
          ))}
        </Card>
      )}
    </div>
  );
}
```

### ColorConverter.tsx — Konverter warna lengkap
```tsx
import { useState } from "react";
import Card from "../../../components/UI/Card";
import Input from "../../../components/UI/Input";
import CopyButton from "../../../components/UI/CopyButton";
import ToolBadge from "../../../components/UI/ToolBadge";

function hexToRgb(hex: string): [number, number, number] | null {
  const result = /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex.trim());
  return result ? [parseInt(result[1], 16), parseInt(result[2], 16), parseInt(result[3], 16)] : null;
}

function rgbToHsl(r: number, g: number, b: number): [number, number, number] {
  r /= 255; g /= 255; b /= 255;
  const max = Math.max(r, g, b), min = Math.min(r, g, b);
  let h = 0, s = 0, l = (max + min) / 2;
  if (max !== min) {
    const d = max - min;
    s = l > 0.5 ? d / (2 - max - min) : d / (max + min);
    switch (max) {
      case r: h = ((g - b) / d + (g < b ? 6 : 0)) / 6; break;
      case g: h = ((b - r) / d + 2) / 6; break;
      case b: h = ((r - g) / d + 4) / 6; break;
    }
  }
  return [Math.round(h * 360), Math.round(s * 100), Math.round(l * 100)];
}

function rgbToCmyk(r: number, g: number, b: number): [number, number, number, number] {
  const R = r / 255, G = g / 255, B = b / 255;
  const k = 1 - Math.max(R, G, B);
  if (k === 1) return [0, 0, 0, 100];
  return [
    Math.round(((1 - R - k) / (1 - k)) * 100),
    Math.round(((1 - G - k) / (1 - k)) * 100),
    Math.round(((1 - B - k) / (1 - k)) * 100),
    Math.round(k * 100),
  ];
}

export default function ColorConverter() {
  const [hex, setHex] = useState("#6d28d9");
  const rgb = hexToRgb(hex);
  const hsl = rgb ? rgbToHsl(...rgb) : null;
  const cmyk = rgb ? rgbToCmyk(...rgb) : null;

  const outputs = rgb && hsl && cmyk ? [
    { label: "HEX", value: hex.toLowerCase(), copy: hex },
    { label: "RGB", value: `rgb(${rgb[0]}, ${rgb[1]}, ${rgb[2]})`, copy: `rgb(${rgb[0]}, ${rgb[1]}, ${rgb[2]})` },
    { label: "HSL", value: `hsl(${hsl[0]}, ${hsl[1]}%, ${hsl[2]}%)`, copy: `hsl(${hsl[0]}, ${hsl[1]}%, ${hsl[2]}%)` },
    { label: "CMYK", value: `cmyk(${cmyk[0]}%, ${cmyk[1]}%, ${cmyk[2]}%, ${cmyk[3]}%)`, copy: `cmyk(${cmyk[0]}%, ${cmyk[1]}%, ${cmyk[2]}%, ${cmyk[3]}%)` },
    { label: "CSS Var", value: `--color-accent: ${hex};`, copy: `--color-accent: ${hex};` },
    { label: "Tailwind", value: `#${hex.replace("#","")}`, copy: hex },
  ] : [];

  return (
    <div className="max-w-2xl mx-auto space-y-4">
      <div className="flex items-start justify-between">
        <div>
          <h2 className="text-2xl font-bold text-white">Konverter Warna</h2>
          <p className="text-gray-400 text-sm mt-1">Konversi HEX ↔ RGB ↔ HSL ↔ CMYK — offline</p>
        </div>
        <ToolBadge type="local" />
      </div>

      <Card className="flex items-center gap-4">
        <div
          className="w-20 h-20 rounded-xl shadow-lg border border-gray-700 flex-shrink-0 cursor-pointer"
          style={{ backgroundColor: rgb ? hex : "#6d28d9" }}
        />
        <div className="flex-1">
          <input
            type="color"
            value={rgb ? hex : "#6d28d9"}
            onChange={(e) => setHex(e.target.value)}
            className="mb-2 w-full h-8 rounded cursor-pointer bg-transparent"
          />
          <Input
            value={hex}
            onChange={(e) => setHex(e.target.value)}
            placeholder="#6d28d9"
            className="font-mono"
          />
        </div>
      </Card>

      {outputs.length > 0 && (
        <div className="grid gap-2">
          {outputs.map((out) => (
            <Card key={out.label} className="flex items-center justify-between py-2">
              <span className="text-gray-500 text-xs w-16">{out.label}</span>
              <code className="text-green-400 font-mono text-sm flex-1 mx-3">{out.value}</code>
              <CopyButton text={out.copy} />
            </Card>
          ))}
        </div>
      )}
    </div>
  );
}
```

---

## 🔑 INSTRUKSI IMPLEMENTASI AKHIR

### WAJIB DILAKUKAN:

1. **Buat semua 260 tools local** dengan JavaScript murni — tidak ada API call sama sekali
2. **Setiap tool AI** harus menggunakan `useAppStore().selectedModel` bukan hardcode model
3. **ModelSelector** harus tampil di Header dan selalu visible
4. **ToolBadge** harus tampil di setiap tool (AI atau Local)
5. **Footer** wajib ada "Powered by Puter" link
6. **Lazy loading** semua tools dengan `React.lazy()` + `Suspense` untuk performa
7. **Fuse.js search** untuk mencari semua 850+ tools berdasarkan nama, deskripsi, tags
8. **Puter KV integration** untuk tools yang butuh persistensi (notepad, tracker, dll)

### MODELS YANG DIGUNAKAN:
- `claude-opus-4-6` — Paling cerdas, untuk tugas kompleks
- `claude-sonnet-4-6` — Lebih cepat, untuk tugas sehari-hari
- Default: `claude-sonnet-4-6`

### CARA PANGGIL AI (WAJIB pakai pattern ini):
```typescript
// Selalu ambil model dari store — JANGAN hardcode!
const { selectedModel } = useAppStore();

// Non-streaming:
const res = await window.puter.ai.chat(prompt, { model: selectedModel });
const text = res.message.content[0].text;

// Streaming:
const stream = await window.puter.ai.chat(prompt, { model: selectedModel, stream: true });
for await (const chunk of stream) {
  const piece = chunk?.text ?? "";
}
```

### CARA BUAT TOOLS LOCAL (WAJIB semua mandiri):
```typescript
// TIDAK BOLEH ADA window.puter.ai.chat() di tools local/
// TIDAK BOLEH ADA fetch() ke external API
// SEMUA logika harus JavaScript browser native
// Boleh menggunakan Web Crypto API, Canvas API, Web Audio API
// Boleh menggunakan CDN library di index.html (qrcode.js, dll)
```

### PRIORITAS BUILD (urutan pengerjaan):
1. Setup proyek: package.json, vite.config.ts, tailwind.config.js, tsconfig.json
2. index.html (dengan Puter.js script tag)
3. src/types/puter.d.ts
4. src/store/useAppStore.ts + toolRegistry.ts
5. src/lib/puter.ts + utils.ts + localUtils.ts
6. src/components/UI/*.tsx (semua 15 komponen)
7. src/components/Layout/*.tsx (Header, Sidebar, Footer, ToolContainer)
8. src/pages/HomePage.tsx + ToolPage.tsx
9. src/App.tsx + src/main.tsx
10. Local tools (260 file) — paralel semua subfolder
11. AI tools (590+ file) — paralel semua subfolder

### TOTAL FILES:
- Config: 5 file
- Types: 1 file
- Store: 2 file
- Lib: 4 file
- Components UI: 15 file
- Components Layout: 4 file
- Pages: 3 file
- Local Tools: ~260 file
- AI Tools: ~590 file
- **TOTAL: ~884 file**

---

## ✅ CHECKLIST SEBELUM SELESAI

- [ ] index.html punya `<script src="https://js.puter.com/v2/"></script>`
- [ ] ModelSelector ada di Header, bisa switch antara claude-opus-4-6 dan claude-sonnet-4-6
- [ ] Setiap AI tool pakai `selectedModel` dari useAppStore (tidak hardcode)
- [ ] Setiap tool punya ToolBadge (AI violet / Local green)
- [ ] Semua 260 local tools berjalan 100% tanpa AI
- [ ] Footer ada "Powered by Puter" link ke https://developer.puter.com
- [ ] Search berfungsi untuk semua 850+ tools
- [ ] Lazy loading tools aktif
- [ ] Sidebar bisa collapse/expand per kategori
- [ ] Tools yang perlu simpan data pakai Puter KV

**MULAI BUILD SEKARANG — SEMUA FILE PARALLEL — NO PLACEHOLDER!**
