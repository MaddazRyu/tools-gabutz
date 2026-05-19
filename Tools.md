
## # ║   PUTERTOOLS V2 - MEGA PLATFORM: AI + NON-AI TOOLS
## ║
# ║   Prompt untuk Replit AI Agent
## ║
# ║   AI Models: claude-opus-4-6 & claude-sonnet-4-6 (pilihan user)
## ║
# ║   Platform: Puter.js (gratis, tanpa API key)
## ║
# ║   Stack: React + TypeScript + Vite + TailwindCSS
## ║
## #
## ╚═════════════════════════════════════════════════════════════════════
## ═════╝

## ---

## ##  INSTRUKSI UTAMA UNTUK REPLIT AI AGENT

Kamu adalah senior full-stack developer. Tugasmu adalah membangun
**PuterTools V2** — sebuah website platform tools raksasa dengan
**600+ AI Tools** dan **250+ Non-AI Tools** yang bisa langsung dipakai
di browser.

## **WAJIB DIBACA SEBELUM MULAI:**
- Baca SEMUA instruksi ini sampai selesai
- Buat SEMUA file secara paralel — jangan skip satu pun
- Setiap file harus FULLY FUNCTIONAL — tidak ada placeholder, tidak
ada TODO
- User bisa MEMILIH model AI: `claude-opus-4-6` atau
## `claude-sonnet-4-6`
- Tools Non-AI harus berjalan 100% offline (tanpa Puter, tanpa API)
- Footer WAJIB ada link "Powered by Puter" →
https://developer.puter.com

## ---

## #
## ╔═════════════════════════════════════════════════════════════════════
## ═════╗

## ##  SETUP PROYEK

### package.json
## ```json
## {
## "name": "putertools-v2",
## "version": "2.0.0",
## "type": "module",
## "scripts": {
## "dev": "vite",
"build": "tsc && vite build",
"preview": "vite preview"
## },
## "dependencies": {
## "react": "^18.3.1",
## "react-dom": "^18.3.1",
## "lucide-react": "^0.400.0",
## "zustand": "^4.5.2",
## "fuse.js": "^7.0.0"
## },
"devDependencies": {
## "@types/react": "^18.3.3",
## "@types/react-dom": "^18.3.0",
## "@vitejs/plugin-react": "^4.3.1",
## "autoprefixer": "^10.4.19",
## "postcss": "^8.4.39",
## "tailwindcss": "^3.4.6",
## "typescript": "^5.5.3",
## "vite": "^5.3.4"
## }
## }

index.html — WAJIB include Puter.js di <head>
<!DOCTYPE html>
<html lang="id">
## <head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width,
initial-scale=1.0" />
<title>PuterTools V2 — 850+ Tools Gratis</title>
<meta name="description" content="Platform 850+ tools gratis: AI
dengan Puter.js + 250+ tools non-AI offline. Pilih model AI
sesukamu!">
## <script
src="[https://js.puter.com/v2/](https://js.puter.com/v2/)"></script>
## </head>

<body class="bg-gray-950 text-white">
<div id="root"></div>
<script type="module" src="/src/main.tsx"></script>
## </body>
## </html>

##  STRUKTUR FOLDER LENGKAP
putertools-v2/
├── index.html
├── package.json
├── vite.config.ts
├── tailwind.config.js
├── tsconfig.json
├── postcss.config.js
## │
└── src/
├── main.tsx
## ├── App.tsx
## │
├── types/
│   └── puter.d.ts           ← TypeScript types untuk Puter.js
## │
├── store/
│   ├── useAppStore.ts       ← Zustand store: navigasi, model AI,
theme
│   └── toolRegistry.ts     ← Daftar semua 850+ tools
## │
├── lib/
│   ├── puter.ts             ← Wrapper semua fungsi Puter.js
│   ├── utils.ts             ← Helper umum (copy, format, dll)
│   ├── localUtils.ts        ← Utility untuk tools non-AI (lokal)
│   └── constants.ts         ← Konstanta global
## │
├── components/
## │   ├── Layout/
│   │   ├── Sidebar.tsx      ← Sidebar navigasi kiri
│   │   ├── Header.tsx       ← Header + model selector
│   │   ├── Footer.tsx       ← Footer dengan "Powered by Puter"
│   │   └── ToolContainer.tsx← Wrapper setiap tool
## │   │
## │   └── UI/
## │       ├── Button.tsx
## │       ├── Input.tsx
## │       ├── Textarea.tsx
## │       ├── Select.tsx

## │       ├── Card.tsx
## │       ├── Badge.tsx
## │       ├── Spinner.tsx
## │       ├── Toast.tsx
## │       ├── Modal.tsx
│       ├── ProgressBar.tsx
│       ├── CopyButton.tsx
│       ├── FileUpload.tsx
│       ├── StreamOutput.tsx
│       ├── ModelSelector.tsx ← BARU: pilih claude-opus-4-6 atau
claude-sonnet-4-6
│       ├── ToolBadge.tsx    ← Badge "AI" atau "Local"
│       └── SearchBar.tsx
## │
├── pages/
│   ├── HomePage.tsx         ← Halaman utama dengan grid semua
tools
│   ├── CategoryPage.tsx     ← Halaman per kategori
│   └── ToolPage.tsx         ← Wrapper render tool aktif
## │
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
## │   │
│   └── local/               ← 250+ TOOLS NON-AI
│       ├── text/            ← 50 tools teks offline
│       ├── converter/       ← 60 tools konverter offline
│       ├── generator/       ← 40 tools generator offline
│       ├── calculator/      ← 50 tools kalkulator offline
│       ├── formatter/       ← 30 tools formatter offline
│       └── utility/         ← 30 tools utility offline


## ⚙ CORE FILES WAJIB
src/types/puter.d.ts
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
## }
## ) => Promise<any>;
txt2img: (prompt: string, options?: { model?: string;
test_mode?: boolean }) => Promise<HTMLImageElement>;
txt2speech: (
text: string,
options?: { provider?: string; voice?: string; language?:
string }
) => Promise<HTMLAudioElement>;
txt2vid: (prompt: string, options?: { test_mode?: boolean })
## => Promise<any>;
img2txt: (file: File | string) => Promise<string>;
speech2txt: (
file: File | Blob,
options?: { model?: string; language?: string; translate?:
boolean }
) => Promise<{ text: string }>;
speech2speech: (
file: File | Blob,
options?: { voice?: string }
## ) => Promise<any>;
listModels: () => Promise<any[]>;
listModelProviders: () => Promise<any[]>;
txt2speech: {
listEngines: () => Promise<any[]>;
listVoices: (provider?: string) => Promise<any[]>;
} & ((text: string, options?: object) =>
Promise<HTMLAudioElement>);
## };
fs: {
write: (path: string, data: any, options?: { overwrite?:
boolean; dedupeName?: boolean }) => Promise<any>;

read: (path: string) => Promise<Blob>;
readdir: (path: string) => Promise<any[]>;
delete: (path: string, options?: { recursive?: boolean }) =>
## Promise<void>;
upload: (file: File | File[], path?: string) => Promise<any>;
getReadURL: (path: string) => Promise<string>;
mkdir: (path: string, options?: { dedupeName?: boolean }) =>
## Promise<any>;
copy: (src: string, dst: string, options?: { overwrite?:
boolean }) => Promise<void>;
move: (src: string, dst: string, options?: { overwrite?:
boolean }) => Promise<void>;
rename: (path: string, newName: string) => Promise<any>;
stat: (path: string) => Promise<any>;
## };
kv: {
set: (key: string, value: any, options?: { ttl?: number }) =>
## Promise<void>;
get: (key: string) => Promise<any>;
del: (key: string) => Promise<void>;
list: (pattern?: string, options?: { values?: boolean }) =>
## Promise<any[]>;
flush: () => Promise<void>;
incr: (key: string, amount?: number) => Promise<number>;
decr: (key: string, amount?: number) => Promise<number>;
add: (key: string, value: any, path?: string) =>
## Promise<void>;
remove: (key: string, path?: string) => Promise<void>;
update: (key: string, updates: Record<string, any>) =>
## Promise<void>;
## };
auth: {
signIn: () => Promise<void>;
signOut: () => Promise<void>;
isSignedIn: () => boolean;
getUser: () => Promise<{ username: string; uuid: string;
email?: string }>;
getMonthlyUsage: () => Promise<any>;
getDetailedAppUsage: (appName: string) => Promise<any>;
## };
hosting: {
create: (subdomain: string, dirPath: string) => Promise<any>;
list: () => Promise<any[]>;
delete: (subdomain: string) => Promise<void>;
update: (subdomain: string, dirPath: string) => Promise<void>;
get: (subdomain: string) => Promise<any>;
## };
workers: {

create: (name: string, file: File) => Promise<any>;
delete: (name: string) => Promise<void>;
list: () => Promise<any[]>;
get: (name: string) => Promise<any>;
exec: (name: string, args?: any) => Promise<any>;
## };
apps: {
create: (options: object) => Promise<any>;
list: () => Promise<any[]>;
delete: (name: string) => Promise<void>;
update: (name: string, options: object) => Promise<any>;
get: (name: string) => Promise<any>;
## };
## };
## }
## }
export {};

src/store/useAppStore.ts — ZUSTAND STORE
import { create } from "zustand";
import { persist } from "zustand/middleware";

export type AIModel = "claude-opus-4-6" | "claude-sonnet-4-6";

export interface AppState {
activeToolId: string;
activeCategoryId: string;
setActiveToolId: (id: string) => void;
setActiveCategoryId: (id: string) => void;

selectedModel: AIModel;
setSelectedModel: (model: AIModel) => void;

searchQuery: string;
setSearchQuery: (q: string) => void;

sidebarOpen: boolean;
setSidebarOpen: (open: boolean) => void;
expandedCategories: string[];
toggleCategory: (id: string) => void;

favorites: string[];
toggleFavorite: (toolId: string) => void;
recentTools: string[];
addRecentTool: (toolId: string) => void;
## }


export const useAppStore = create<AppState>()(
persist(
(set, get) => ({
activeToolId: "",
activeCategoryId: "",
setActiveToolId: (id) => {
set({ activeToolId: id });
get().addRecentTool(id);
## },
setActiveCategoryId: (id) => set({ activeCategoryId: id }),

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
## });
## },

favorites: [],
toggleFavorite: (toolId) => {
const current = get().favorites;
set({
favorites: current.includes(toolId)
? current.filter((id) => id !== toolId)
: [...current, toolId],
## });
## },

recentTools: [],
addRecentTool: (toolId) => {
const current = get().recentTools.filter((id) => id !==
toolId);
set({ recentTools: [toolId, ...current].slice(0, 10) });
## },
## }),

{ name: "putertools-v2-store" }
## )
## );

src/lib/puter.ts — WRAPPER HELPER
import { useAppStore } from "../store/useAppStore";

export function getActiveModel(): string {
return useAppStore.getState().selectedModel;
## }

export async function aiChat(prompt: string, modelOverride?: string):
## Promise<string> {
const model = modelOverride ?? getActiveModel();
const res = await window.puter.ai.chat(prompt, { model });
return res.message.content[0].text;
## }

export async function* aiStream(prompt: string, modelOverride?:
string): AsyncGenerator<string> {
const model = modelOverride ?? getActiveModel();
const stream = await window.puter.ai.chat(prompt, { model, stream:
true });
for await (const chunk of stream) {
yield chunk?.text ?? "";
## }
## }

export async function* aiStreamWithHistory(
messages: { role: "user" | "assistant"; content: string }[],
modelOverride?: string
): AsyncGenerator<string> {
const model = modelOverride ?? getActiveModel();
const stream = await window.puter.ai.chat(messages, { model, stream:
true });
for await (const chunk of stream) {
yield chunk?.text ?? "";
## }
## }

export async function generateImage(prompt: string):
Promise<HTMLImageElement> {
return window.puter.ai.txt2img(prompt, { model: "gpt-image-2" });
## }

export async function textToSpeech(

text: string,
options?: { provider?: string; voice?: string }
): Promise<HTMLAudioElement> {
return window.puter.ai.txt2speech(text, { provider: "openai",
## ...options });
## }

export async function speechToText(file: File, translate = false):
## Promise<string> {
const result = await window.puter.ai.speech2txt(file, { translate
## });
return result.text;
## }

export async function imageToText(file: File): Promise<string> {
return window.puter.ai.img2txt(file);
## }

export async function kvSet(key: string, value: any): Promise<void> {
await window.puter.kv.set(key, JSON.stringify(value));
## }

export async function kvGet<T>(key: string): Promise<T | null> {
try {
const val = await window.puter.kv.get(key);
return val ? JSON.parse(val) : null;
} catch {
return null;
## }
## }

export async function kvDel(key: string): Promise<void> {
await window.puter.kv.del(key);
## }

export async function fsWrite(path: string, data: string):
## Promise<void> {
await window.puter.fs.write(path, data, { overwrite: true });
## }

export async function fsRead(path: string): Promise<string> {
const blob = await window.puter.fs.read(path);
return await blob.text();
## }

export function isSignedIn(): boolean {
return window.puter.auth.isSignedIn();
## }


export async function signIn(): Promise<void> {
await window.puter.auth.signIn();
## }

src/components/UI/ModelSelector.tsx
import { useAppStore, AIModel } from "../../store/useAppStore";

const MODELS: { value: AIModel; label: string; desc: string; badge:
string }[] = [
## {
value: "claude-sonnet-4-6",
label: "Claude Sonnet 4.6",
desc: "Cepat & efisien — cocok untuk sehari-hari",
badge: "⚡ Cepat",
## },
## {
value: "claude-opus-4-6",
label: "Claude Opus 4.6",
desc: "Paling cerdas — cocok untuk tugas kompleks",
badge: "易 Terkuat",
## },
## ];

export default function ModelSelector() {
const { selectedModel, setSelectedModel } = useAppStore();

return (
<div className="flex items-center gap-2">
<span className="text-gray-400 text-xs whitespace-nowrap">Model
AI:</span>
<div className="flex bg-gray-800 rounded-lg p-0.5 gap-0.5">
{MODELS.map((m) => (
## <button
key={m.value}
onClick={() => setSelectedModel(m.value)}
title={m.desc}
className={`px-3 py-1.5 rounded-md text-xs font-medium
transition-all duration-200 ${
selectedModel === m.value
? "bg-violet-600 text-white shadow-lg
shadow-violet-900/50"
: "text-gray-400 hover:text-white hover:bg-gray-700"
## }`}
## >
{m.badge} {m.value === "claude-opus-4-6" ? "Opus" :

"Sonnet"}
## </button>
## ))}
## </div>
## </div>
## );
## }

烙 TEMPLATE TOOL AI (Wajib untuk semua 600+
tools AI)
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
const DISCLAIMER = "";

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
## Input: ${input}
Berikan output terstruktur, berguna, dan langsung to the point dalam
## Bahasa Indonesia.`;


const stream = await window.puter.ai.chat(prompt, {
model: selectedModel,
stream: true,
## });

let fullText = "";
for await (const chunk of stream) {
fullText += chunk?.text ?? "";
setOutput(fullText);
## }
} catch (err: unknown) {
setError("Error: " + (err instanceof Error ? err.message :
## String(err)));
} finally {
setLoading(false);
setStreaming(false);
## }
## };

return (
<div className="max-w-3xl mx-auto space-y-4">
<div className="flex items-start justify-between">
## <div>
<h2 className="text-2xl font-bold
text-white">{TOOL_NAME}</h2>
<p className="text-gray-400 mt-1 text-sm">{TOOL_DESC}</p>
## {DISCLAIMER && (
<p className="text-yellow-400 text-xs mt-2 p-2
bg-yellow-500/10 rounded-lg border border-yellow-500/20">
## ⚠ {DISCLAIMER}
## </p>
## )}
## </div>
<ToolBadge type="ai" model={selectedModel} />
## </div>

<Card>
<Textarea
value={input}
onChange={(e) => setInput(e.target.value)}
placeholder="Masukkan input di sini..."
rows={4}
disabled={loading}
## />
{error && <p className="text-red-400 text-sm
mt-2">{error}</p>}
<Button onClick={handleGenerate} disabled={loading ||

!input.trim()} className="mt-3 w-full">
{loading ? <Spinner /> : "✨ Generate"}
</Button>
</Card>

## {output && (
<Card>
<div className="flex justify-between items-center mb-2">
<span className="text-gray-400 text-xs">Hasil
({selectedModel}):</span>
<CopyButton text={output} />
## </div>
<StreamOutput text={output} streaming={streaming} />
</Card>
## )}
## </div>
## );
## }

 TEMPLATE TOOL NON-AI (Untuk semua 250+ tools
lokal)
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
const result = input.toUpperCase(); // GANTI LOGIKA SESUAI TOOL
setOutput(result);
} catch (err) {

setError("Error: " + String(err));
## }
## };

return (
<div className="max-w-3xl mx-auto space-y-4">
<div className="flex items-start justify-between">
## <div>
<h2 className="text-2xl font-bold
text-white">{TOOL_NAME}</h2>
<p className="text-gray-400 mt-1 text-sm">{TOOL_DESC}</p>
## </div>
<ToolBadge type="local" />
## </div>

<Card>
<Input
value={input}
onChange={(e) => setInput(e.target.value)}
placeholder="Masukkan input..."
## />
{error && <p className="text-red-400 text-sm
mt-2">{error}</p>}
<Button onClick={handleProcess} disabled={!input.trim()}
className="mt-3 w-full">
##  Proses
</Button>
</Card>

## {output && (
<Card>
<div className="flex justify-between items-center mb-2">
<span className="text-gray-400 text-xs">Hasil
(Offline):</span>
<CopyButton text={output} />
## </div>
<pre className="text-green-400 text-sm font-mono
whitespace-pre-wrap break-words bg-gray-900 p-3 rounded-lg">
## {output}
## </pre>
</Card>
## )}
## </div>
## );
## }


##  DAFTAR LENGKAP SEMUA TOOLS (850+ FITUR)
## ══════════════════════════════════
KATEGORI 1-16: 烙 AI TOOLS (600+ Tools)
## ══════════════════════════════════
KATEGORI 1: ✍ TOOLS MENULIS (52 tools)
File: src/tools/writing/
- ArticleWriter.tsx - Buat artikel blog panjang dari topik
- BlogPostGenerator.tsx - Generator postingan blog SEO-friendly
- EssayWriter.tsx - Penulis esai akademik/formal
- StoryWriter.tsx - Penulis cerita fiksi/cerpen
- NovelChapter.tsx - Generator bab novel
- ScriptWriter.tsx - Penulis skrip film/YouTube/podcast
- Paraphraser.tsx - Parafrasa teks agar berbeda
- Summarizer.tsx - Ringkasan teks panjang
- GrammarChecker.tsx - Koreksi tata bahasa
- SpellChecker.tsx - Koreksi ejaan
- ToneChanger.tsx - Ubah nada tulisan (formal/casual/friendly)
- TextExpander.tsx - Perluas teks pendek jadi panjang
- TextShortener.tsx - Persingkat teks panjang
- ParagraphWriter.tsx - Buat paragraf dari ide
- IntroductionWriter.tsx - Buat kalimat/paragraf pembuka
- ConclusionWriter.tsx - Buat kesimpulan dari teks
- HeadlineGenerator.tsx - Buat judul yang menarik
- SubheadingGenerator.tsx - Buat sub-judul konten
- MetaDescWriter.tsx - Buat meta deskripsi SEO
- ProductDescription.tsx - Deskripsi produk e-commerce
- BioWriter.tsx - Buat bio profil (Instagram/LinkedIn/Twitter)
- CoverLetter.tsx - Surat lamaran kerja
- ResumeWriter.tsx - Buat resume/CV
- EmailWriter.tsx - Buat email profesional
- EmailReply.tsx - Balas email dengan AI
- EmailSubjectLine.tsx - Buat subject email yang menarik
- NewsletterWriter.tsx - Buat konten newsletter
- PressRelease.tsx - Buat siaran pers
- ProposalWriter.tsx - Buat proposal bisnis/proyek
- ReportWriter.tsx - Buat laporan formal
- MeetingNotes.tsx - Rangkum catatan meeting
- MemoWriter.tsx - Buat memo internal
- PolicyWriter.tsx - Buat kebijakan/SOP
- JobDescription.tsx - Buat deskripsi lowongan kerja

- PerformanceReview.tsx - Buat penilaian kinerja karyawan
- ThankYouNote.tsx - Buat ucapan terima kasih
- ApologyLetter.tsx - Buat surat permintaan maaf
- ComplaintLetter.tsx - Buat surat keluhan
- RecommendationLetter.tsx - Buat surat rekomendasi
- PoemWriter.tsx - Buat puisi dari tema
- LyricsWriter.tsx - Buat lirik lagu
- JokeGenerator.tsx - Buat lelucon/humor
- QuoteGenerator.tsx - Buat kutipan inspiratif
- MottoGenerator.tsx - Buat motto/tagline
- SloganGenerator.tsx - Buat slogan brand
- CTAWriter.tsx - Buat Call-to-Action yang convert
- LandingPageCopy.tsx - Teks halaman landing page
- AboutUsWriter.tsx - Buat halaman "Tentang Kami"
- FAQGenerator.tsx - Buat daftar FAQ
- TestimonialWriter.tsx - Buat testimonial palsu realistis
- TranslatorTool.tsx - Terjemahan ke 100+ bahasa
- LanguageDetector.tsx - Deteksi bahasa teks
KATEGORI 2:  TOOLS KONTEN KREATOR (55 tools)
File: src/tools/content/
- ViralAnalyzer.tsx - Analisis timestamp viral YouTube
- YouTubeScriptWriter.tsx - Buat skrip video YouTube
- YouTubeTitleGenerator.tsx - Buat judul YouTube yang clickbait
- YouTubeDescWriter.tsx - Buat deskripsi video YouTube
- YouTubeTagsGenerator.tsx - Buat tags/keyword YouTube
- YouTubeThumbnailIdea.tsx - Ide desain thumbnail YouTube
- YouTubeHookWriter.tsx - Buat hook 3 detik pembuka video
- YouTubeEndscreen.tsx - Skrip penutup/outro video
- TikTokScriptWriter.tsx - Buat skrip video TikTok
- TikTokHookGenerator.tsx - Buat hook TikTok yang viral
- TikTokCaptionWriter.tsx - Buat caption TikTok + hashtag
- TikTokTrendAnalyzer.tsx - Analisis tren TikTok dari topik
- InstagramCaptionWriter.tsx- Buat caption Instagram
- InstagramBioWriter.tsx - Buat bio Instagram
- InstagramHashtags.tsx - Generator hashtag Instagram relevan
- InstagramCarouselScript.tsx- Skrip konten carousel Instagram
- ReelsScriptWriter.tsx - Skrip video Reels
- PodcastOutlineWriter.tsx - Buat outline episode podcast
- PodcastIntroWriter.tsx - Buat intro podcast
- PodcastShowNotes.tsx - Buat show notes podcast
- PodcastQuestions.tsx - Buat pertanyaan wawancara podcast
- ContentCalendar.tsx - Buat kalender konten 30 hari
- ContentIdeasGenerator.tsx - Generator 100 ide konten
- NicheAnalyzer.tsx - Analisis niche yang profitable
- CompetitorAnalysis.tsx - Analisis kompetitor konten

- AudiencePersona.tsx - Buat persona audiens target
- StorytellingFramework.tsx - Framework cerita untuk konten
- ViralHookFormulas.tsx - 50 formula hook viral
- ContentRepurposer.tsx - Ubah 1 konten jadi 10 format
- ThreadWriter.tsx - Buat Twitter/X thread
- LinkedInPostWriter.tsx - Buat postingan LinkedIn
- LinkedInArticleWriter.tsx - Buat artikel LinkedIn panjang
- FacebookPostWriter.tsx - Buat postingan Facebook
- WhatsAppBroadcast.tsx - Buat pesan broadcast WhatsApp
- TelegramPost.tsx - Buat konten channel Telegram
- PinterestDescription.tsx - Buat deskripsi pin Pinterest
- ProductReviewWriter.tsx - Buat review produk
- UnboxingScript.tsx - Skrip video unboxing
- TutorialScriptWriter.tsx - Skrip video tutorial
- MotivationalContent.tsx - Konten motivasi/inspirasi
- MemeTextGenerator.tsx - Buat teks meme
- ClickbaitTitle.tsx - Generator judul clickbait
- StorytellingPost.tsx - Buat konten storytelling
- BeforeAfterContent.tsx - Format konten before/after
- ListicleWriter.tsx - Buat artikel daftar (listicle)
- CaseStudyWriter.tsx - Buat studi kasus
- InterviewQnA.tsx - Format konten Q&A
- MiniCoursOutline.tsx - Buat outline mini kursus
- ChallengeIdeas.tsx - Ide challenge viral
- GiveawayPost.tsx - Buat postingan giveaway
- PollQuestions.tsx - Buat pertanyaan polling
- AMAQuestions.tsx - Buat pertanyaan AMA (Ask Me Anything)
- SponsoredContentWriter.tsx- Buat konten sponsored/iklan
- AffiliateCopyWriter.tsx - Buat copy konten affiliate
- ReviewResponseWriter.tsx - Balas ulasan/komentar negatif
KATEGORI 3:  TOOLS GAMBAR (32 tools)
File: src/tools/image/
- ImageGenerator.tsx - Generate gambar dari teks (gpt-image-2)
- LogoConceptGenerator.tsx - Buat konsep/prompt logo
- ThumbnailGenerator.tsx - Generate thumbnail YouTube
- BannerGenerator.tsx - Generate banner iklan
- SocialMediaImageGen.tsx - Generate gambar sosmed berbagai size
- ProductMockupPrompt.tsx - Prompt untuk mockup produk
- InfographicPrompt.tsx - Prompt untuk infografis
- IllustrationPrompt.tsx - Prompt ilustrasi karakter
- BackgroundRemoverDesc.tsx- Deskripsi cara hapus background
- ImagePromptEnhancer.tsx - Perbaiki prompt gambar agar lebih baik
- StableDiffusionPrompt.tsx- Buat prompt Stable Diffusion
- MidjourneyPrompt.tsx - Buat prompt Midjourney
- DALLEPromptWriter.tsx - Buat prompt DALL-E optimal

- ImageAltTextWriter.tsx - Buat alt text gambar untuk SEO
- ImageCaptionWriter.tsx - Buat caption untuk gambar
- ImageAnalyzer.tsx - Analisis isi gambar (OCR + deskripsi) via img2txt
- PhotoEditingIdeas.tsx - Ide editing foto untuk konten
- ColorPaletteGenerator.tsx- Generate palet warna dari deskripsi
- FontPairingAdvisor.tsx - Rekomendasi pasangan font
- DesignFeedback.tsx - Feedback desain dari deskripsi
- BrandIdentityGuide.tsx - Buat panduan identitas brand
- IconPromptGenerator.tsx - Prompt untuk icon set
- PatternPromptGenerator.tsx- Prompt untuk pattern/tekstur
- WallpaperPrompt.tsx - Prompt wallpaper
- BookCoverPrompt.tsx - Prompt cover buku
- AlbumCoverPrompt.tsx - Prompt sampul album musik
- PosterPrompt.tsx - Prompt desain poster
- MemeTemplateIdea.tsx - Ide template meme
- QRCodeIdeas.tsx - Ide desain QR code artistik
- EmojiSetPrompt.tsx - Prompt untuk set emoji custom
- AvatarPrompt.tsx - Prompt untuk avatar/profile picture
- NFTArtPrompt.tsx - Prompt untuk NFT art
KATEGORI 4:  TOOLS AUDIO (28 tools)
File: src/tools/audio/
- TextToSpeech.tsx - Konversi teks ke suara
- SpeechToText.tsx - Transkripsi audio ke teks
- AudioTranslator.tsx - Transkripsi + terjemah audio
- PodcastTranscriber.tsx - Transkripsi episode podcast
- MeetingTranscriber.tsx - Transkripsi rekaman meeting
- LectureTranscriber.tsx - Transkripsi kuliah/seminar
- SpeechSummarizer.tsx - Ringkas isi audio/podcast
- VoiceNoteToEmail.tsx - Ubah voice note jadi email formal
- VoiceNoteToTask.tsx - Ekstrak tugas dari voice note
- InterviewTranscriber.tsx - Transkripsi wawancara
- AudioPrompter.tsx - Buat skrip untuk rekaman suara
- VoiceoverScript.tsx - Skrip untuk voice over video
- AudiobookScript.tsx - Buat skrip audiobook dari teks
- RadioScriptWriter.tsx - Skrip iklan radio
- SongLyricsAnalyzer.tsx - Analisis makna lirik lagu
- MusicPromptGenerator.tsx - Prompt untuk AI music generator (Suno/Udio)
- SoundEffectPrompt.tsx - Prompt untuk sound effect
- PodcastIntroScript.tsx - Buat skrip intro podcast
- JingleWriter.tsx - Buat lirik jingle iklan
- ASMR.ScriptWriter.tsx - Skrip konten ASMR
- AudioDescriptionWriter.tsx- Buat deskripsi audio untuk video
- SpeechCoachFeedback.tsx - Feedback naskah pidato
- PresentationScript.tsx - Skrip presentasi
- SpeechDebateArgument.tsx - Argumen untuk debat/pidato

- DubScript.tsx - Buat skrip dubbing
- SubtitleWriter.tsx - Buat subtitle dari transkripsi
- SRTFormatter.tsx - Format transkripsi ke .SRT subtitle
- AudioTrimPrompt.tsx - Rekomendasi kapan harus trim audio
KATEGORI 5:  TOOLS VIDEO (22 tools)
File: src/tools/video/
- VideoScriptWriter.tsx - Skrip video lengkap dengan scene
- VideoOutlineCreator.tsx - Outline video step-by-step
- VideoHookWriter.tsx - Hook 3-5 detik pertama video
- VideoTransitionIdeas.tsx - Ide transisi antar scene
- B-RollIdeas.tsx - Ide footage B-roll untuk video
- VideoTitleABTest.tsx - A/B test judul video
- VideoEndScreenScript.tsx - Skrip end screen/outro
- ViralAnalyzerYoutube.tsx - Analisis potensi viral YouTube
- ShortsScriptWriter.tsx - Skrip YouTube Shorts/Reels
- VideoAdScript.tsx - Skrip iklan video (30/60 detik)
- EducationalVideoScript.tsx- Skrip video edukasi
- DocumentaryScript.tsx - Skrip dokumenter pendek
- StoryboardTextCreator.tsx- Buat storyboard teks per scene
- VideoDescriptionWriter.tsx- Deskripsi video YouTube SEO
- VideoChapterMarkers.tsx - Buat chapter markers YouTube
- VideoCallToAction.tsx - CTA untuk akhir video
- VideoCritique.tsx - Kritik/feedback skrip video
- WatchTimeOptimizer.tsx - Tips optimasi watch time
- ThumbnailABTest.tsx - A/B test konsep thumbnail
- VideoSeriesPlanner.tsx - Rencanakan seri video
- ShortFormStrategy.tsx - Strategi konten short-form
- VideoRepurposer.tsx - Ubah video panjang jadi multi-format
KATEGORI 6:  TOOLS DEVELOPER (62 tools)
File: src/tools/developer/
- CodeExplainer.tsx - Jelaskan kode yang membingungkan
- CodeReviewer.tsx - Review kode + saran perbaikan
- CodeDebugger.tsx - Debug error + solusi
- CodeConverter.tsx - Konversi kode antar bahasa
- CodeOptimizer.tsx - Optimasi performa kode
- CodeDocGenerator.tsx - Buat dokumentasi kode
- CodeCommentWriter.tsx - Tambahkan komentar ke kode
- RegexGenerator.tsx - Generate regex dari deskripsi
- SQLQueryWriter.tsx - Buat query SQL dari bahasa alami
- SQLOptimizer.tsx - Optimasi query SQL
- APIDocWriter.tsx - Buat dokumentasi API
- READMEWriter.tsx - Buat README.md project

- GitCommitMessage.tsx - Buat pesan commit Git yang baik
- GitIgnoreGenerator.tsx - Buat .gitignore untuk tech stack
- DockerfileGenerator.tsx - Buat Dockerfile
- CICDPipelineWriter.tsx - Buat config CI/CD
- EnvFileGenerator.tsx - Template .env file
- UnitTestWriter.tsx - Buat unit test dari kode
- MockDataGenerator.tsx - Generate mock/dummy data JSON
- JSONFormatter.tsx - Format + validasi JSON
- JSONtoCSV.tsx - Konversi JSON ke CSV (lokal)
- CSVtoJSON.tsx - Konversi CSV ke JSON (lokal)
- XMLFormatter.tsx - Format + validasi XML
- MarkdownEditor.tsx - Editor Markdown dengan preview
- HTMLGenerator.tsx - Buat HTML dari deskripsi
- CSSGenerator.tsx - Buat CSS dari deskripsi desain
- TailwindConverter.tsx - Konversi CSS biasa ke Tailwind
- JSFunctionWriter.tsx - Buat fungsi JavaScript
- PythonFunctionWriter.tsx - Buat fungsi Python
- AlgorithmExplainer.tsx - Jelaskan algoritma
- DataStructureExplainer.tsx- Jelaskan struktur data
- DesignPatternAdvisor.tsx - Rekomendasi design pattern
- ArchitectureAdvisor.tsx - Rekomendasi arsitektur sistem
- SecurityChecker.tsx - Cek kerentanan keamanan kode
- PerformanceTips.tsx - Tips optimasi performa web
- AccessibilityChecker.tsx - Cek aksesibilitas UI dari deskripsi
- SEOTechAudit.tsx - Audit teknis SEO
- PWAChecklist.tsx - Checklist Progressive Web App
- APIEndpointDesigner.tsx - Desain endpoint API RESTful
- DatabaseSchemaDesigner.tsx- Desain skema database
- ERDiagramTextCreator.tsx - Buat ER diagram dalam teks
- SystemDesignHelper.tsx - Bantu desain sistem skala besar
- TechStackAdvisor.tsx - Rekomendasi tech stack untuk proyek
- DependencyAnalyzer.tsx - Analisis package.json
- ErrorMessageExplainer.tsx- Jelaskan error message
- LogAnalyzer.tsx - Analisis log aplikasi
- CodeSnippetLibrary.tsx - Koleksi snippet code berguna
- TerminalCommandHelper.tsx- Buat perintah terminal/bash
- LinuxCommandExplainer.tsx- Jelaskan perintah Linux
- CronJobGenerator.tsx - Buat ekspresi cron job
- WebhookHelper.tsx - Buat handler webhook
- GraphQLHelper.tsx - Buat query/mutation GraphQL
- SocketIOHelper.tsx - Kode Socket.io dasar
- LocalStorageHelper.tsx - Manajemen localStorage (lokal)
- CookieManager.tsx - Manajemen cookie (lokal)
- ColorCodeConverter.tsx - Konversi HEX/RGB/HSL (lokal)
- Base64Tool.tsx - Encode/decode Base64 (lokal)
- HashGenerator.tsx - Generate hash MD5/SHA (lokal)
- URLEncoder.tsx - Encode/decode URL (lokal)
- JWTDecoder.tsx - Decode JWT token (lokal)

- TimestampConverter.tsx - Konversi Unix timestamp (lokal)
- UUIDGenerator.tsx - Generate UUID (lokal)
KATEGORI 7:  TOOLS SEO (42 tools)
File: src/tools/seo/
- KeywordResearch.tsx - Riset keyword dari topik
- KeywordCluster.tsx - Kelompokkan keyword serupa
- LongTailKeyword.tsx - Temukan keyword long-tail
- KeywordDifficulty.tsx - Estimasi kesulitan keyword
- SearchIntentAnalyzer.tsx - Analisis intent keyword
- LSIKeywordGenerator.tsx - Generator keyword LSI
- KeywordGapAnalysis.tsx - Analisis gap keyword vs kompetitor
- TitleTagOptimizer.tsx - Optimasi title tag halaman
- MetaDescOptimizer.tsx - Optimasi meta deskripsi
- URLSlugGenerator.tsx - Buat URL slug SEO-friendly
- HeaderStructurePlanner.tsx- Rencana struktur H1/H2/H3
- ContentBriefWriter.tsx - Buat content brief untuk penulis
- SEOContentOutline.tsx - Outline konten SEO
- FeaturedSnippetOptimizer.tsx- Optimasi untuk featured snippet
- SchemaMarkupGenerator.tsx- Buat schema markup JSON-LD
- FAQSchemaWriter.tsx - Buat FAQ schema markup
- BreadcrumbSchema.tsx - Buat breadcrumb schema
- LocalSEOOptimizer.tsx - Optimasi SEO lokal
- GBPDescWriter.tsx - Deskripsi Google Business Profile
- BacklinkOutreachEmail.tsx - Email outreach backlink
- GuestPostPitch.tsx - Pitch artikel tamu
- InternalLinkingStrategy.tsx- Strategi internal linking
- AnchorTextGenerator.tsx - Generator anchor text natural
- CompetitorContentGap.tsx - Analisis gap konten vs kompetitor
- TopicClusterPlanner.tsx - Rencanakan topic cluster
- PillarPageOutline.tsx - Outline halaman pilar
- ContentAuditHelper.tsx - Panduan audit konten lama
- RedirectMapper.tsx - Rencana redirect 301
- SitemapPlanner.tsx - Rencana struktur sitemap
- RobotstxtGenerator.tsx - Buat robots.txt
- HreflangHelper.tsx - Buat tag hreflang
- PageSpeedTips.tsx - Tips optimasi PageSpeed
- CoreWebVitals.tsx - Penjelasan dan tips Core Web Vitals
- E-E-A-TChecker.tsx - Audit E-E-A-T konten
- SEOAuditChecklist.tsx - Checklist audit SEO lengkap
- LocalCitationTemplate.tsx- Template NAP citations
- GoogleAdsKeyword.tsx - Riset keyword Google Ads
- AdCopyWriter.tsx - Buat teks iklan Google/Meta Ads
- ABTestHeadline.tsx - A/B test headline iklan
- LandingSEOAudit.tsx - Audit SEO landing page
- EcomSEOOptimizer.tsx - Optimasi SEO e-commerce

- BlogSEOOptimizer.tsx - Optimasi SEO artikel blog
KATEGORI 8:  TOOLS SOSIAL MEDIA (48 tools)
File: src/tools/social/
- SocialMediaScheduler.tsx - Buat jadwal posting mingguan
- ContentMixStrategy.tsx - Strategi mix konten 80/20
- EngagementBooster.tsx - Tips tingkatkan engagement
- CommunityReplyWriter.tsx - Buat balasan komentar komunitas
- DM.TemplateWriter.tsx - Template DM/pesan pribadi
- CrisisResponseWriter.tsx - Tangani krisis di sosmed
- BrandVoiceGuide.tsx - Buat panduan brand voice
- SocialMediaBio.tsx - Buat bio untuk semua platform
- ProfileOptimizer.tsx - Optimasi profil sosmed
- HashtagStrategy.tsx - Strategi hashtag per platform
- HashtagGrouper.tsx - Kelompokkan hashtag per niche
- TrendHijacker.tsx - Manfaatkan tren untuk konten
- ViralPostFormula.tsx - Formula postingan viral
- StoryIdeas.tsx - Ide konten Instagram/Facebook Story
- PollCreator.tsx - Buat konten polling interaktif
- QuizCreator.tsx - Buat kuis untuk engagement
- GiveawayRules.tsx - Buat aturan giveaway resmi
- CollabPitch.tsx - Pitch kolaborasi ke kreator lain
- SponsorPitch.tsx - Pitch ke sponsor/brand
- MediaKit.tsx - Buat media kit konten kreator
- PricingCard.tsx - Buat rate card endorsement
- InfluencerBrief.tsx - Brief untuk influencer
- UGCCampaign.tsx - Buat kampanye user-generated content
- ViralChallenge.tsx - Buat challenge viral
- CountdownPost.tsx - Konten countdown event
- LaunchPost.tsx - Konten peluncuran produk
- AnniversaryPost.tsx - Konten ulang tahun brand
- MotivationalMonday.tsx - Konten Motivational Monday
- TestimonialPost.tsx - Konten testimonial customer
- EmployeeSpotlight.tsx - Konten sorotan karyawan
- BehindTheScenes.tsx - Konten behind the scenes
- ProductLaunchPlan.tsx - Rencana konten launch produk
- MemorialDayPost.tsx - Konten hari besar nasional
- SeasonalContent.tsx - Konten musiman/hari raya
- EngagementQuestion.tsx - Pertanyaan yang memancing engage
- SocialListeningReport.tsx- Template laporan social listening
- CompetitorSocialAudit.tsx- Audit sosmed kompetitor
- GrowthHackingTips.tsx - Tips growth hacking sosmed
- CrossPlatformStrategy.tsx- Strategi cross-platform
- VideoShortStrategy.tsx - Strategi konten video pendek
- PodcastGrowthPlan.tsx - Rencana pertumbuhan podcast
- NewsletterGrowth.tsx - Strategi tumbuhkan subscriber

- CommunityBuilding.tsx - Panduan bangun komunitas online
- SocialAuditReport.tsx - Laporan audit akun sosmed
- ROI.Calculator.tsx - Kalkulasi ROI sosmed (lokal)
- FollowerAnalysis.tsx - Analisis tipe follower
- PostTimingAdvisor.tsx - Rekomendasi waktu posting
- EngagementRateCalc.tsx - Kalkulator engagement rate (lokal)
KATEGORI 9: ⚡ TOOLS PRODUKTIVITAS (50 tools)
File: src/tools/productivity/
- TaskBreakdown.tsx - Pecah proyek besar jadi tugas kecil
- PriorityMatrix.tsx - Buat matriks prioritas Eisenhower
- GoalSetter.tsx - Buat SMART goals
- OKRWriter.tsx - Buat OKR (Objectives & Key Results)
- ProjectPlan.tsx - Buat rencana proyek
- MeetingAgenda.tsx - Buat agenda meeting
- MeetingSummary.tsx - Ringkas notulen meeting
- ActionItems.tsx - Ekstrak action items dari teks
- DecisionMatrix.tsx - Buat matriks keputusan
- ProsConsAnalyzer.tsx - Analisis pro dan kontra
- SWOT.Analyzer.tsx - Analisis SWOT dari deskripsi bisnis
- BrainstormHelper.tsx - Fasilitasi sesi brainstorming
- MindMapCreator.tsx - Buat mind map teks
- ProcessMapper.tsx - Buat peta proses/alur kerja
- SOPWriter.tsx - Buat Standard Operating Procedure
- ChecklistCreator.tsx - Buat checklist dari proses
- TimerPlanner.tsx - Jadwal kerja Pomodoro (lokal)
- HabitTracker.tsx - Tracker kebiasaan harian (lokal + KV)
- JournalPrompts.tsx - Prompt jurnal harian
- DailyPlanner.tsx - Buat rencana harian terstruktur
- WeeklyReview.tsx - Template review mingguan
- MonthlyReview.tsx - Template review bulanan
- YearlyGoalPlanner.tsx - Rencana tujuan tahunan
- PersonalMission.tsx - Buat pernyataan misi pribadi
- TimeAudit.tsx - Audit penggunaan waktu
- EnergyMapper.tsx - Peta energi produktivitas harian
- FocusBooster.tsx - Tips meningkatkan fokus
- DistractionBlocker.tsx - Rencana blokir distraksi
- DeepWorkSchedule.tsx - Jadwal deep work
- EmailInboxZero.tsx - Strategi inbox zero
- FileNamingSystem.tsx - Sistem penamaan file
- FolderStructure.tsx - Buat struktur folder yang rapi
- NoteOrganizer.tsx - Sistem organisasi catatan
- ReadingList.tsx - Buat daftar baca terstruktur
- BookSummary.tsx - Ringkas buku dari judul/deskripsi
- ArticleSummarizer.tsx - Ringkas artikel dari paste teks
- DocumentSummarizer.tsx - Ringkas dokumen panjang

- ReportSummarizer.tsx - Ringkas laporan
- PresentationOutline.tsx - Buat outline presentasi
- PresentationScript.tsx - Skrip presentasi slide per slide
- PitchDeckOutline.tsx - Outline pitch deck startup
- Speechwriter.tsx - Buat naskah pidato
- TalkingPoints.tsx - Buat talking points untuk presentasi
- NegotiationScript.tsx - Skrip negosiasi
- ConflictResolution.tsx - Panduan resolusi konflik
- FeedbackScript.tsx - Skrip memberikan feedback konstruktif
- DelegationGuide.tsx - Panduan delegasi tugas
- OnboardingPlan.tsx - Rencana onboarding karyawan baru
- TrainingPlan.tsx - Rencana pelatihan
- KPIBuilder.tsx - Buat KPI untuk departemen/individu
KATEGORI 10:  TOOLS PENDIDIKAN (40 tools)
File: src/tools/education/
- ExplainLikeFive.tsx - Jelaskan topik kompleks dengan mudah
- ConceptExplainer.tsx - Jelaskan konsep ilmiah
- HistoryStoryteller.tsx - Ceritakan sejarah dengan menarik
- MathSolver.tsx - Bantu selesaikan soal matematika
- PhysicsSolver.tsx - Bantu fisika dengan penjelasan
- ChemistrySolver.tsx - Bantu kimia dengan penjelasan
- BiologyExplainer.tsx - Jelaskan biologi
- GeographyHelper.tsx - Helper geografi
- QuizGenerator.tsx - Buat kuis dari materi
- FlashcardCreator.tsx - Buat flashcard belajar
- StudyGuideWriter.tsx - Buat panduan belajar
- EssayOutline.tsx - Outline esai akademik
- ThesisStatement.tsx - Buat thesis statement
- CitationFormatter.tsx - Format sitasi (APA/MLA/Chicago)
- LiteratureReview.tsx - Panduan menulis tinjauan pustaka
- ResearchQuestions.tsx - Buat pertanyaan penelitian
- MethodologyHelper.tsx - Panduan metodologi penelitian
- AbstractWriter.tsx - Buat abstrak penelitian
- DebateArguments.tsx - Argumen untuk debat
- CriticalThinkingHelper.tsx- Pertanyaan berpikir kritis
- AnalogiesGenerator.tsx - Buat analogi untuk pemahaman
- MemoryTechniques.tsx - Teknik menghafal (mnemonik)
- LearningPathCreator.tsx - Buat jalur belajar mandiri
- CourseOutlineWriter.tsx - Buat outline kursus online
- LessonPlanWriter.tsx - Buat rencana pelajaran (RPP)
- AssignmentCreator.tsx - Buat tugas/assignment
- RubricCreator.tsx - Buat rubrik penilaian
- FeedbackOnEssay.tsx - Feedback pada esai siswa
- TranslateAndExplain.tsx - Terjemah + penjelasan kosakata
- GrammarLesson.tsx - Pelajaran tata bahasa

- VocabularyBuilder.tsx - Builder kosakata bahasa asing
- PronunciationGuide.tsx - Panduan pengucapan
- LanguageLearningPlan.tsx - Rencana belajar bahasa
- IELTSEssayHelper.tsx - Bantuan esai IELTS/TOEFL
- CodingTutor.tsx - Tutor coding untuk pemula
- ScienceProjectIdeas.tsx - Ide proyek sains
- BookReport.tsx - Buat book report
- PresentationFeedback.tsx - Feedback presentasi
- MockInterview.tsx - Simulasi wawancara kerja
- ScholarshipEssay.tsx - Esai beasiswa
KATEGORI 11:  TOOLS BISNIS (42 tools)
File: src/tools/business/
- BusinessIdeaGenerator.tsx- Generator ide bisnis
- BusinessPlanWriter.tsx - Buat business plan
- ExecutiveSummary.tsx - Buat executive summary
- MarketResearch.tsx - Riset pasar dari niche
- TAMCalculator.tsx - Hitung TAM/SAM/SOM
- CompetitorMatrix.tsx - Matriks perbandingan kompetitor
- ValueProposition.tsx - Buat value proposition
- USPFinder.tsx - Temukan Unique Selling Proposition
- PricingStrategy.tsx - Strategi penetapan harga
- PricingTable.tsx - Buat tabel paket harga
- RevenueModel.tsx - Buat model pendapatan
- BusinessModelCanvas.tsx - Isi Business Model Canvas
- CustomerJourneyMap.tsx - Buat peta perjalanan customer
- PainPointAnalyzer.tsx - Analisis pain point pelanggan
- SolutionFitChecker.tsx - Cek problem-solution fit
- ProductMarketFit.tsx - Evaluasi product-market fit
- GTMStrategy.tsx - Strategi go-to-market
- LaunchChecklist.tsx - Checklist peluncuran produk/bisnis
- InvestorPitch.tsx - Buat pitch ke investor
- FundingProposal.tsx - Proposal pendanaan
- GrantApplicationHelper.tsx- Bantu proposal hibah
- PartnershipProposal.tsx - Proposal kemitraan bisnis
- MOUDraft.tsx - Draft Memorandum of Understanding
- ContractTemplate.tsx - Template kontrak dasar
- InvoiceTemplate.tsx - Template faktur (lokal)
- QuotationTemplate.tsx - Template penawaran harga
- ProjectProposal.tsx - Proposal proyek ke klien
- CaseStudyTemplate.tsx - Template studi kasus pelanggan
- CustomerFeedbackAnalysis.tsx- Analisis feedback pelanggan
- NPSAnalyzer.tsx - Analisis Net Promoter Score
- SupportTicketResponse.tsx- Buat respons tiket support
- RefundEmailWriter.tsx - Email kebijakan refund
- TermsOfService.tsx - Draft Syarat & Ketentuan

- PrivacyPolicy.tsx - Draft Kebijakan Privasi
- HR.JobPostingWriter.tsx - Buat posting lowongan kerja
- InterviewQuestions.tsx - Buat pertanyaan wawancara HRD
- OfferLetterWriter.tsx - Buat surat penawaran kerja
- TerminationLetter.tsx - Surat pemutusan hubungan kerja
- WarningLetter.tsx - Surat peringatan karyawan
- CompanyAnnouncement.tsx - Pengumuman internal perusahaan
- BudgetTemplate.tsx - Template anggaran (lokal)
- ROICalculator.tsx - Kalkulasi ROI proyek (lokal)
KATEGORI 12:  TOOLS DATA & ANALITIK (30 tools)
File: src/tools/data/
- DataInterpreter.tsx - Interpretasi data/angka dari paste
- ChartDescriber.tsx - Deskripsikan data untuk chart
- SurveyAnalyzer.tsx - Analisis hasil survei
- StatisticsExplainer.tsx - Jelaskan statistik
- TrendAnalyzer.tsx - Analisis tren dari data
- AnomalyDetector.tsx - Deteksi anomali dari data paste
- CorrelationFinder.tsx - Temukan korelasi dalam data
- DataCleaner.tsx - Panduan bersihkan data kotor
- DataStoryTeller.tsx - Ubah data jadi narasi
- ExecutiveReport.tsx - Buat laporan eksekutif dari data
- KPIDashboard.tsx - Buat template KPI dashboard
- MetricsDefinition.tsx - Definisikan metrik bisnis
- FunnelAnalysis.tsx - Analisis funnel konversi
- CohortAnalysis.tsx - Jelaskan cohort analysis
- AttributionModeling.tsx - Model atribusi marketing
- CustomerSegmentation.tsx - Segmentasi pelanggan
- RFMAnalysis.tsx - Analisis RFM pelanggan
- ChurnPrediction.tsx - Prediksi churn pelanggan
- LTV.Calculator.tsx - Hitung Customer Lifetime Value (lokal)
- CAC.Calculator.tsx - Hitung Customer Acquisition Cost (lokal)
- BreakevenCalculator.tsx - Kalkulasi break-even point (lokal)
- FinancialRatioCalc.tsx - Kalkulator rasio keuangan (lokal)
- PivotTableHelper.tsx - Bantu membuat pivot table
- DashboardDesignTips.tsx - Tips desain dashboard
- DataVisualizationAdvisor.tsx- Pilih jenis chart yang tepat
- ABTestCalculator.tsx - Kalkulasi statistik A/B test (lokal)
- SampleSizeCalc.tsx - Hitung ukuran sampel (lokal)
- HypothesisTester.tsx - Buat hipotesis penelitian
- DataETL.Explainer.tsx - Jelaskan proses ETL
- BigDataConcepts.tsx - Jelaskan konsep big data
KATEGORI 13:  TOOLS KESEHATAN (20 tools)

File: src/tools/health/
- SymptomChecker.tsx - Cek gejala + rekomendasi (dengan disclaimer)
- MedicationReminder.tsx - Buat jadwal minum obat
- NutritionAnalyzer.tsx - Analisis kandungan gizi makanan
- MealPlanGenerator.tsx - Buat rencana makan sehat
- WorkoutPlanGenerator.tsx - Buat rencana olahraga
- BMI.Calculator.tsx - Kalkulator BMI (lokal)
- CalorieCalculator.tsx - Kalkulator kalori harian (lokal)
- WaterIntakeCalc.tsx - Kebutuhan air harian (lokal)
- SleepScheduler.tsx - Jadwal tidur optimal
- StressReliefTips.tsx - Tips manajemen stres
- MeditationScript.tsx - Skrip meditasi terpandu
- MentalHealthJournal.tsx - Prompt jurnal kesehatan mental
- AnxietyReliefTips.tsx - Tips redakan kecemasan
- FirstAidGuide.tsx - Panduan pertolongan pertama
- VaccineSchedule.tsx - Jadwal vaksinasi (info umum)
- PregnancyInfo.tsx - Info kehamilan (dengan disclaimer)
- BabyDevMilestones.tsx - Milestone perkembangan bayi
- FitnessGoalSetter.tsx - Buat target kebugaran
- RecoveryPlan.tsx - Rencana pemulihan cedera
- HealthChecklistYearly.tsx- Checklist kesehatan tahunan
KATEGORI 14: ⚖ TOOLS HUKUM (20 tools)
File: src/tools/legal/
- ContractAnalyzer.tsx - Analisis kontrak + risiko
- LegalTermExplainer.tsx - Jelaskan istilah hukum
- NDAdraft.tsx - Draft Non-Disclosure Agreement
- FreelanceContract.tsx - Kontrak freelancer
- RentalAgreement.tsx - Perjanjian sewa-menyewa
- EmploymentContract.tsx - Kontrak kerja dasar
- ServiceAgreement.tsx - Perjanjian layanan
- DisputeLetterWriter.tsx - Surat sengketa/keberatan
- ConsumerRightsGuide.tsx - Panduan hak konsumen Indonesia
- IP.ProtectionGuide.tsx - Panduan perlindungan HKI
- CopyrightGuide.tsx - Panduan hak cipta
- TrademarkSearch.tsx - Panduan cari merek dagang
- StartupLegalChecklist.tsx- Checklist legal startup
- PTFoundingGuide.tsx - Panduan pendirian PT Indonesia
- UMKMLegalGuide.tsx - Panduan legal UMKM Indonesia
- TaxObligationGuide.tsx - Panduan kewajiban pajak (info umum)
- LaborLawSummary.tsx - Ringkasan UU Ketenagakerjaan
- DataPrivacyCompliance.tsx- Panduan kepatuhan privasi data
- EcommerceRegulation.tsx - Regulasi e-commerce Indonesia
- CyberCrimeLaw.tsx - Info hukum kejahatan siber Indonesia

KATEGORI 15:  TOOLS KEUANGAN (22 tools)
File: src/tools/finance/
- BudgetPlanner.tsx - Buat anggaran bulanan (lokal + KV)
- SavingsCalculator.tsx - Kalkulator tabungan (lokal)
- LoanCalculator.tsx - Kalkulator cicilan KPR/KTA (lokal)
- InvestmentCalculator.tsx - Kalkulator investasi compound (lokal)
- RetirementPlanner.tsx - Planner dana pensiun (lokal)
- EmergencyFund.tsx - Hitung dana darurat (lokal)
- DebtPayoffPlanner.tsx - Rencana pelunasan hutang (lokal)
- NetWorthCalculator.tsx - Kalkulator kekayaan bersih (lokal)
- InvestmentExplainer.tsx - Jelaskan instrumen investasi
- StockAnalysisHelper.tsx - Bantu analisis saham dasar
- CryptoExplainer.tsx - Jelaskan cryptocurrency
- DeFiExplainer.tsx - Jelaskan DeFi
- MutualFundExplainer.tsx - Jelaskan reksa dana
- InsuranceAdvisor.tsx - Panduan pilih asuransi
- TaxPlanning.tsx - Tips perencanaan pajak
- FreelanceTaxGuide.tsx - Panduan pajak freelancer
- FinancialGoals.tsx - Buat tujuan keuangan SMART
- ExpenseTracker.tsx - Tracker pengeluaran (lokal + KV)
- FinancialLiteracy.tsx - Kuis literasi keuangan
- SideHustleIdeas.tsx - Ide penghasilan sampingan
- PassiveIncomeGuide.tsx - Panduan passive income
- FinancialPlan.tsx - Buat rencana keuangan pribadi
KATEGORI 16:  TOOLS HIBURAN & FUN (25 tools)
File: src/tools/fun/
- StoryGenerator.tsx - Buat cerita interaktif
- RPGStoryCreator.tsx - Buat skenario game RPG
- JokeGenerator.tsx - Generator lelucon
- RiddleCreator.tsx - Buat teka-teki
- TriviaQuizMaker.tsx - Buat kuis trivia
- WordGameCreator.tsx - Buat permainan kata
- ScavengerHuntCreator.tsx - Buat tantangan scavenger hunt
- IcebreakerQuestions.tsx - Pertanyaan ice breaker
- PartyGameIdeas.tsx - Ide permainan pesta
- WouldYouRather.tsx - Generator pertanyaan "Would You Rather"
- HoroscopeWriter.tsx - Buat horoskop kreatif
- FortuneCookie.tsx - Buat pesan fortune cookie
- ComicStrip.tsx - Buat skrip komik strip
- FanFictionWriter.tsx - Buat fan fiction
- WorldBuilding.tsx - Buat dunia fiksi
- CharacterCreator.tsx - Buat karakter fiksi detail

- DialogueWriter.tsx - Buat dialog antar karakter
- DreamInterpreter.tsx - Interpretasi mimpi (fun, bukan serius)
- PersonalityAnalyzer.tsx - Analisis kepribadian dari deskripsi
- CompatibilityChecker.tsx - Cek kompatibilitas (fun)
- BucketListCreator.tsx - Buat bucket list
- TravelItinerary.tsx - Buat rencana perjalanan wisata
- RecipeGenerator.tsx - Buat resep dari bahan yang ada
- MovieRecommender.tsx - Rekomendasi film dari preferensi
- BookRecommender.tsx - Rekomendasi buku
## ══════════════════════════════════
KATEGORI 17-22: ⚡ LOCAL TOOLS (250+ Tools Offline)
## ══════════════════════════════════
 LOCAL/TEXT — 50 Tools Manipulasi Teks Offline
File: src/tools/local/text/
- WordCounter.tsx - Hitung kata, karakter, kalimat, paragraf secara real-time
- CharacterCounter.tsx - Counter karakter dengan batas maksimum (Twitter, SMS, dll)
- TextReverser.tsx - Balik urutan teks / per kata / per kalimat
- TextSorter.tsx - Urutkan baris teks (A-Z, Z-A, random, panjang)
- DuplicateLineRemover.tsx - Hapus baris duplikat dari teks
- EmptyLineRemover.tsx - Hapus baris kosong dari teks
- LineNumberAdder.tsx - Tambah nomor baris ke setiap baris teks
- TextCaseConverter.tsx - Ubah case: UPPER, lower, Title, camelCase, snake_case,
PascalCase, kebab-case, SCREAMING_SNAKE
- WhitespaceRemover.tsx - Hapus spasi berlebih, tab, whitespace
- TextTrimmer.tsx - Trim kiri, kanan, atau kedua sisi setiap baris
- FindAndReplace.tsx - Cari dan ganti teks (support regex)
- TextDiff.tsx - Bandingkan dua teks, tampilkan perbedaan
- TextMerger.tsx - Gabungkan banyak blok teks dengan separator
- TextSplitter.tsx - Pecah teks berdasarkan karakter/kata/kalimat/paragraf
- TextExtractor.tsx - Ekstrak email, URL, nomor telepon, angka dari teks
- TextRandomizer.tsx - Acak urutan baris teks
- TextRepeat.tsx - Ulangi teks N kali
- PalindromeChecker.tsx - Cek apakah kata/kalimat adalah palindrom
- AnagramChecker.tsx - Cek apakah dua kata adalah anagram
- VowelConsonantCounter.tsx - Hitung vokal dan konsonan
- SentenceLengthAnalyzer.tsx - Analisis panjang setiap kalimat
- ReadingTimeEstimator.tsx - Estimasi waktu baca teks (WPM)
- UniqueWordCounter.tsx - Hitung kata unik dan frekuensinya
- MostFrequentWords.tsx - Tampilkan N kata paling sering muncul
- TextToList.tsx - Ubah teks paragraf jadi list berpoin

- ListToText.tsx - Gabung list jadi teks paragraf
- CSVtoTable.tsx - Render CSV sebagai tabel HTML visual
- TextSlug.tsx - Ubah judul/teks jadi URL slug (lowercase, tanpa spasi)
- TextCleaner.tsx - Bersihkan teks dari karakter spesial/HTML entities
- HTMLEntityEncoder.tsx - Encode/decode HTML entities (&, <, dll)
- TextTruncator.tsx - Potong teks pada N karakter/kata dengan ellipsis
- ColumnExtractor.tsx - Ekstrak kolom tertentu dari teks terstruktur/CSV
- LineJoiner.tsx - Gabung semua baris jadi satu baris
- AddPrefix.tsx - Tambah prefix ke setiap baris teks
- AddSuffix.tsx - Tambah suffix ke setiap baris teks
- TextStripper.tsx - Hapus semua HTML tags dari teks
- PunctuationRemover.tsx - Hapus semua tanda baca dari teks
- DigitExtractor.tsx - Ekstrak semua angka dari teks
- LetterExtractor.tsx - Ekstrak hanya huruf dari teks
- SpecialCharRemover.tsx - Hapus karakter non-ASCII / spesial
- AsciiArtGenerator.tsx - Buat ASCII art dari teks (figlet-style)
- TextToMorse.tsx - Konversi teks ke kode Morse (dan sebaliknya)
- TextToBinary.tsx - Konversi teks ke biner (0s dan 1s) dan sebaliknya
- TextToHex.tsx - Konversi teks ke hex dan sebaliknya
- TextToAscii.tsx - Tampilkan nilai ASCII setiap karakter
- SpaceToTab.tsx - Konversi spasi ke tab dan sebaliknya
- TextPadder.tsx - Pad teks ke kiri/kanan/tengah dengan karakter pilihan
- StringInterpolator.tsx - Template string sederhana: ganti {variabel} dengan nilai
- TextStatistics.tsx - Statistik lengkap teks: Flesch score, avg sentence, dll
- LoremIpsumGenerator.tsx - Generate Lorem Ipsum dalam berbagai panjang
 LOCAL/CONVERTER — 60 Tools Konverter Offline
File: src/tools/local/converter/
- JSONFormatter.tsx - Format/minify/validasi JSON dengan syntax highlighting
- JSONtoCSV.tsx - Konversi array JSON ke format CSV
- CSVtoJSON.tsx - Konversi CSV ke format JSON
- JSONtoYAML.tsx - Konversi JSON ke YAML
- YAMLtoJSON.tsx - Konversi YAML ke JSON
- JSONtoXML.tsx - Konversi JSON ke XML
- XMLtoJSON.tsx - Konversi XML ke JSON sederhana
- XMLFormatter.tsx - Format/minify/validasi XML
- MarkdownToHTML.tsx - Konversi Markdown ke HTML (parser lokal)
- HTMLToMarkdown.tsx - Konversi HTML ke Markdown
- CSVtoHTML.tsx - Konversi CSV ke tabel HTML
- JSONtoTable.tsx - Render JSON array sebagai tabel HTML interaktif
- Base64Encoder.tsx - Encode teks/file ke Base64
- Base64Decoder.tsx - Decode Base64 ke teks/file
- URLEncoder.tsx - Encode/decode URL (encodeURIComponent)
- URLParser.tsx - Parsing URL: protocol, host, path, params, hash
- QueryStringBuilder.tsx - Build dan parse query string URL
- JWTDecoder.tsx - Decode payload JWT token (tanpa verifikasi)

- Base32Encoder.tsx - Encode/decode Base32
- HexToRGB.tsx - Konversi warna: HEX ↔ RGB ↔ HSL ↔ HSV
- ColorConverter.tsx - Konverter warna lengkap: HEX, RGB, HSL, HSV, CMYK, CSS
- NumberBaseConverter.tsx - Konversi bilangan: Desimal ↔ Biner ↔ Oktal ↔ Hex
- RomanNumeralConverter.tsx - Konversi angka Arab ↔ Angka Romawi
- TemperatureConverter.tsx - Celsius ↔ Fahrenheit ↔ Kelvin ↔ Rankine
- LengthConverter.tsx - Konversi satuan panjang: cm, m, km, inch, ft, mile, dll
- WeightConverter.tsx - Konversi satuan berat: kg, g, lb, oz, stone, dll
- VolumeConverter.tsx - Konversi satuan volume: ml, L, gallon, pint, cup, dll
- AreaConverter.tsx - Konversi satuan luas: m², km², ft², acre, hectare, dll
- SpeedConverter.tsx - Konversi kecepatan: km/h, m/s, mph, knot, dll
- DataSizeConverter.tsx - Konversi ukuran data: bit, byte, KB, MB, GB, TB, PB
- TimeZoneConverter.tsx - Konversi waktu antar timezone dunia
- UnixTimestampConverter.tsx - Konversi Unix timestamp ↔ tanggal manusia
- DateFormatConverter.tsx - Konversi format tanggal: DD/MM/YYYY ↔ YYYY-MM-DD ↔
dll
- DurationConverter.tsx - Konversi durasi: detik ↔ menit ↔ jam ↔ hari
- CurrencyFormatter.tsx - Format angka sebagai mata uang berbagai negara (offline)
- NumberFormatter.tsx - Format angka: ribuan, desimal, ilmiah, persen
- FractionConverter.tsx - Konversi desimal ↔ pecahan (0.5 → 1/2)
- AngleConverter.tsx - Konversi sudut: derajat ↔ radian ↔ gradian
- PressureConverter.tsx - Konversi tekanan: Pa, bar, psi, atm, dll
- EnergyConverter.tsx - Konversi energi: Joule, kWh, kalori, BTU, dll
- PowerConverter.tsx - Konversi daya: Watt, kW, HP, dll
- StorageConverter.tsx - Konversi penyimpanan file dengan breakdown lengkap
- PixelRemConverter.tsx - Konversi px ↔ rem ↔ em ↔ pt ↔ vw/vh (CSS)
- ImageResolutionCalc.tsx - Hitung resolusi: PPI, DPI untuk ukuran cetak
- AspectRatioCalc.tsx - Hitung dan konversi aspect ratio (16:9, 4:3, dll)
- CSStoSCSS.tsx - Konversi CSS biasa ke format SCSS sederhana
- HEXtoRGBA.tsx - HEX + alpha → rgba() CSS
- GradientsConverter.tsx - Konversi gradient CSS antar format
- SoundUnitConverter.tsx - Konversi satuan suara: dB, amplitude, dll
- FuelEconomyConverter.tsx - Konversi konsumsi BBM: L/100km ↔ MPG ↔ km/L
- CookingConverter.tsx - Konversi satuan memasak: cup, tbsp, tsp, ml, gram
- NutritionConverter.tsx - Konversi unit nutrisi: kkal, kJ, IU, mcg
- ResolutionConverter.tsx - Konversi resolusi layar dan pixel density
- FrequencyConverter.tsx - Konversi frekuensi: Hz, kHz, MHz, GHz
- VoltageConverter.tsx - Konversi tegangan listrik dan daya
- ResistanceConverter.tsx - Konversi hambatan: Ohm, kΩ, MΩ
- MagneticConverter.tsx - Konversi satuan magnet: Tesla, Gauss
- PrintSizeCalculator.tsx - Hitung ukuran cetak dari pixel + DPI
- ColorsNameFinder.tsx - Temukan nama warna dari kode HEX
- PantoneToHex.tsx - Referensi konversi warna Pantone ↔ HEX
⚡ LOCAL/GENERATOR — 40 Tools Generator Offline
File: src/tools/local/generator/

- PasswordGenerator.tsx - Generate password kuat dengan aturan kustom
- PINGenerator.tsx - Generate PIN numerik dengan panjang pilihan
- UUIDGenerator.tsx - Generate UUID v1/v4 dalam jumlah banyak
- NanoIDGenerator.tsx - Generate NanoID dengan alphabet dan panjang kustom
- RandomStringGenerator.tsx - Generate string acak: huruf, angka, simbol
- RandomNumberGenerator.tsx - Generate angka acak dalam rentang dengan distribusi
- HashGenerator.tsx - Hitung hash: MD5, SHA-1, SHA-256, SHA-512 (Web Crypto)
- HMACGenerator.tsx - Generate HMAC-SHA256 dari key + message
- ChecksumCalculator.tsx - Hitung checksum CRC32, Adler32
- QRCodeGenerator.tsx - Generate QR Code dari teks/URL (library qrcode.js CDN)
- BarcodeGenerator.tsx - Generate barcode: EAN-13, Code128, QR (CDN)
- FaviconGenerator.tsx - Generate favicon SVG sederhana dari teks/emoji
- AvatarGenerator.tsx - Generate avatar placeholder berdasarkan nama (canvas)
- GravatarURL.tsx - Generate URL Gravatar dari email (hash MD5)
- PlaceholderImageURL.tsx - Generate URL placeholder image (via.placeholder.com)
- ColorPaletteGenerator.tsx - Generate palet warna harmonis dari satu warna dasar
- GradientGenerator.tsx - Generator gradient CSS dengan preview langsung
- ShadowGenerator.tsx - Generator box-shadow CSS dengan preview
- BorderRadiusGenerator.tsx - Generator border-radius CSS visual
- FontScaleGenerator.tsx - Generate skala tipografi (major third, golden ratio, dll)
- LineHeightCalc.tsx - Hitung line-height optimal dari font size
- GridSystemGenerator.tsx - Generate grid CSS custom (columns, gap, dll)
- FlexboxGenerator.tsx - Visual builder flexbox CSS
- CSSAnimationGenerator.tsx - Generator keyframe CSS animation
- CSSSelectorGenerator.tsx - Helper menulis CSS selector kompleks
- FakeEmailGenerator.tsx - Generate email palsu realistis (random name + domain)
- FakeNameGenerator.tsx - Generate nama palsu Indonesia/internasional
- FakePhoneGenerator.tsx - Generate nomor telepon Indonesia acak (format valid)
- FakeAddressGenerator.tsx - Generate alamat palsu Indonesia
- MockJSONGenerator.tsx - Generate JSON dummy dari schema sederhana
- RegexGenerator.tsx - Build regex dari deskripsi pattern visual
- RegexTester.tsx - Test regex dengan input dan lihat matches
- CronExpressionGenerator.tsx - Build ekspresi cron secara visual
- CronExpressionExplainer.tsx - Jelaskan cron expression dalam bahasa manusia
- ColorSchemeGenerator.tsx - Generate color scheme: monochromatic, complementary,
triadic
- SymbolLibrary.tsx - Kumpulan simbol Unicode, emoji, arrows — copy dengan klik
- EmojiPicker.tsx - Emoji picker dengan kategori dan search
- HTMLColorCodes.tsx - Referensi semua named CSS colors dengan preview
- DataURIGenerator.tsx - Encode file/teks ke Data URI (base64 inline)
- SVGPatternGenerator.tsx - Generate pola SVG: dots, stripes, crosshatch, dll
燐 LOCAL/CALCULATOR — 50 Tools Kalkulator Offline
File: src/tools/local/calculator/
- ScientificCalculator.tsx - Kalkulator saintifik lengkap: sin/cos/tan, log, sqrt, exp
- PercentageCalculator.tsx - Hitung persentase: X% dari Y, X adalah berapa% dari Y

- DiscountCalculator.tsx - Hitung harga setelah diskon + berapa hemat
- TaxCalculator.tsx - Hitung pajak PPN/PPh dari harga
- TipCalculator.tsx - Hitung tip restoran dan bagi per orang
- BMICalculator.tsx - Hitung BMI + kategori (underweight/normal/obese)
- BMRCalculator.tsx - Hitung Basal Metabolic Rate (Harris-Benedict)
- TDEECalculator.tsx - Hitung Total Daily Energy Expenditure
- IdealWeightCalculator.tsx - Hitung berat badan ideal (berbagai formula)
- BodyFatCalculator.tsx - Estimasi body fat percentage dari pengukuran
- CalorieCalculator.tsx - Hitung kalori harian berdasarkan tujuan (defisit/surplus)
- MacroCalculator.tsx - Hitung kebutuhan protein, karbohidrat, lemak harian
- WaterIntakeCalculator.tsx - Hitung kebutuhan air harian (berdasarkan berat + aktivitas)
- SleepCalculator.tsx - Hitung waktu tidur optimal berdasarkan siklus 90 menit
- AgeCalculator.tsx - Hitung usia tepat dalam tahun, bulan, hari, jam
- DateDifferenceCalc.tsx - Hitung selisih antar dua tanggal
- DaysUntilCalc.tsx - Hitung hari hingga tanggal tertentu (ulang tahun, event)
- LoanCalculator.tsx - Kalkulator cicilan KPR/KTA: angsuran, total bayar, bunga
- MortgageCalculator.tsx - Kalkulator KPR detail dengan tabel amortisasi
- CompoundInterestCalc.tsx - Kalkulator bunga majemuk investasi
- SimpleSavingsCalc.tsx - Simulasi tabungan dengan bunga sederhana
- RetirementCalculator.tsx - Estimasi dana pensiun berdasarkan target
- EmergencyFundCalc.tsx - Hitung kebutuhan dana darurat (3-12 bulan)
- InvestmentROICalc.tsx - Hitung Return on Investment
- NetWorthCalc.tsx - Hitung kekayaan bersih: aset - liabilitas
- BudgetSplitter.tsx - Bagi anggaran berdasarkan aturan 50/30/20
- SplitBillCalculator.tsx - Bagi tagihan ke beberapa orang (+ tip, pajak)
- CurrencyPctChange.tsx - Hitung perubahan persentase harga/nilai
- BreakevenCalculator.tsx - Hitung titik impas bisnis
- ProfitMarginCalc.tsx - Hitung profit margin (gross, net, operating)
- MarkupCalculator.tsx - Hitung markup harga dari HPP
- FrequencyCalc.tsx - Kalkulator frekuensi & panjang gelombang fisika
- OhmsLawCalculator.tsx - Kalkulator hukum Ohm: V=IR
- PowerCalculator.tsx - Kalkulator daya listrik: P=VI
- ElectricityBillCalc.tsx - Estimasi tagihan listrik dari pemakaian watt
- FuelCostCalculator.tsx - Hitung biaya BBM perjalanan (jarak + konsumsi)
- SpeedDistanceTimeCalc.tsx - Kalkulator kecepatan/jarak/waktu
- TravelTimeCalc.tsx - Estimasi waktu perjalanan dari jarak + kecepatan
- TypingSpeedCalc.tsx - Hitung WPM dari jumlah kata + waktu ketik
- ReadSpeedCalc.tsx - Hitung kecepatan baca (WPM) dari teks + waktu
- GradeCalculator.tsx - Hitung nilai akhir dari beberapa komponen + bobot
- GPACalculator.tsx - Hitung GPA dari daftar mata kuliah + nilai + SKS
- PaceCalculator.tsx - Kalkulator pace lari: min/km dari jarak & waktu
- CalorieBurnCalc.tsx - Estimasi kalori terbakar per aktivitas olahraga
- PregnancyDueDateCalc.tsx - Hitung HPL dari HPHT (Hari Pertama Haid Terakhir)
- OvulationCalc.tsx - Estimasi masa subur dari siklus menstruasi
- FibonacciGenerator.tsx - Generate deret Fibonacci hingga N suku
- PrimeChecker.tsx - Cek apakah angka prima + faktorisasi prima
- FactorialCalc.tsx - Hitung faktorial dan kombinasi/permutasi
- StatisticsCalculator.tsx - Hitung: mean, median, modus, std dev, variance dari dataset

 LOCAL/FORMATTER — 30 Tools Formatter & Prettifier Offline
File: src/tools/local/formatter/
- SQLFormatter.tsx - Format/beautify SQL query dengan indentasi rapi
- CSSFormatter.tsx - Format/minify CSS
- HTMLFormatter.tsx - Format/minify/validasi HTML
- JavaScriptFormatter.tsx - Format/minify JavaScript (basic)
- JSONDiffViewer.tsx - Bandingkan dua JSON, tampilkan perbedaan
- MarkdownPreview.tsx - Editor Markdown + live preview HTML
- HTMLPreview.tsx - Tulis HTML, lihat preview langsung di iframe
- CSSPreview.tsx - Tulis CSS, lihat hasil live (dengan div contoh)
- SVGEditor.tsx - Editor SVG dengan preview langsung
- RegexVisualizer.tsx - Visualisasi matches regex di teks dengan highlight
- JSONPathTester.tsx - Test JSONPath expression di JSON object
- XPathTester.tsx - Test XPath sederhana di XML
- CSSGradientPreview.tsx - Preview gradient CSS langsung dari kode
- BoxShadowPreview.tsx - Preview box-shadow CSS dari kode
- TextShadowPreview.tsx - Preview text-shadow CSS dari kode
- BorderPreview.tsx - Preview border CSS (style, width, color, radius)
- TransformPreview.tsx - Preview CSS transform: rotate, scale, skew, translate
- AnimationPreview.tsx - Preview CSS animation/keyframes sederhana
- FontPreview.tsx - Preview teks dengan Google Font pilihan
- ColorContrastChecker.tsx - Cek kontras warna foreground vs background (WCAG)
- AccessibilityColorHelper.tsx - Cek aksesibilitas kombinasi warna (AA/AAA)
- GridVisualizer.tsx - Visualisasikan CSS Grid dari kode grid-template
- FlexboxVisualizer.tsx - Visualisasikan layout flexbox dari kode flex
- SpacingPreview.tsx - Preview margin/padding dengan visual box model
- EasingPreview.tsx - Preview CSS easing function (curve visualization)
- NumberFormat.tsx - Preview berbagai format angka: comma, dot, space separator
- DateFormatPreview.tsx - Preview format tanggal dari berbagai pattern
- CSSVariablesExtractor.tsx - Ekstrak semua CSS variables (--var) dari kode
- TailwindToCSS.tsx - Konversi Tailwind class ke CSS properties lengkap
- CSSSpecificityCalc.tsx - Hitung specificity selector CSS (a, b, c)
 LOCAL/UTILITY — 30 Tools Utility & Developer Tools Offline
File: src/tools/local/utility/
- LocalStorageManager.tsx - Lihat, edit, hapus localStorage & sessionStorage browser
- CookieManager.tsx - Lihat dan hapus cookies di browser saat ini
- ColorPickerTool.tsx - Color picker lengkap: pilih warna, salin semua format
- ScreenResolutionInfo.tsx - Info layar: resolusi, DPR, viewport, orientasi
- UserAgentParser.tsx - Parse User Agent: browser, OS, device type
- IPAddressInfo.tsx - Info IP lokal + format + validasi
- MACAddressGenerator.tsx - Generate MAC address acak + format
- SubnetCalculator.tsx - Kalkulator subnet IPv4: network, broadcast, host range

- PortNumberReference.tsx - Referensi port terkenal (HTTP=80, HTTPS=443, dll)
- HTTPStatusCodes.tsx - Referensi semua HTTP status code + deskripsi
- MIMETypeReference.tsx - Referensi MIME type berdasarkan ekstensi file
- CharsetReference.tsx - Referensi karakter set: UTF-8, ASCII, Latin-1
- KeycodeViewer.tsx - Tampilkan keycode, key, dan code saat tekan tombol
- ClipboardHistory.tsx - Riwayat clipboard session (simpan di memory)
- CountdownTimer.tsx - Timer hitung mundur dengan suara alert
- Stopwatch.tsx - Stopwatch dengan lap time
- WorldClock.tsx - Jam digital multi-timezone (tidak perlu API)
- MetronomeApp.tsx - Metronom digital dengan BPM kustom (Web Audio API)
- PomodoroClock.tsx - Timer Pomodoro 25/5 dengan notifikasi
- FlashcardApp.tsx - Flashcard interaktif dengan KV store (simpan ke Puter)
- NotepadApp.tsx - Notepad sederhana dengan auto-save ke Puter KV
- MarkdownNotes.tsx - Catatan Markdown yang tersimpan di Puter KV
- BookmarkManager.tsx - Simpan bookmark/link di Puter KV
- TaskListApp.tsx - Todo list sederhana tersimpan di Puter KV
- HabitTracker.tsx - Tracker kebiasaan harian dengan visualisasi calendar
- ExpenseTracker.tsx - Tracker pengeluaran sederhana dengan kategori
- BudgetApp.tsx - Aplikasi budget bulanan sederhana (Puter KV)
- PasswordManager.tsx - Password manager lokal (tersimpan terenkripsi di Puter KV)
- DiceRoller.tsx - Dadu digital: d4, d6, d8, d10, d12, d20, custom
- CoinFlipper.tsx - Lempar koin dengan animasi dan statistik
 TOOL REGISTRY (src/store/toolRegistry.ts)
Buat registry lengkap SEMUA tools (850+) dengan struktur:
export type Tool = {
id: string;
label: string;
description: string;
category: string;
type: "ai" | "local";
tags?: string[];
component: () => Promise<{ default: React.ComponentType }>;
## };

export const ALL_TOOLS: Tool[] = [
## // ===== AI TOOLS =====
## {
id: "article-writer",
label: "Penulis Artikel",
description: "Buat artikel blog panjang dari topik",
category: "writing",
type: "ai",
tags: ["tulis", "blog", "konten"],
component: () => import("../tools/writing/ArticleWriter"),
## },

// ... semua 600+ AI tools

## // ===== LOCAL TOOLS =====
## {
id: "word-counter",
label: "Penghitung Kata",
description: "Hitung kata, karakter, kalimat secara real-time",
category: "local-text",
type: "local",
tags: ["kata", "teks", "counter", "offline"],
component: () => import("../tools/local/text/WordCounter"),
## },
// ... semua 260 local tools
## ];

export const CATEGORIES = [
// 16 kategori AI ...
## {
id: "local",
icon: "",
label: "Local Tools",
description: "250+ tools offline, tanpa AI, tanpa internet",
badge: "⚡ Offline",
color: "green",
subCategories: [
{ id: "local-text", label: "Teks", icon: "", count: 50 },
{ id: "local-converter", label: "Konverter", icon: "", count:
## 60 },
{ id: "local-generator", label: "Generator", icon: "⚡", count:
## 40 },
{ id: "local-calculator", label: "Kalkulator", icon: "燐",
count: 50 },
{ id: "local-formatter", label: "Formatter", icon: "", count:
## 30 },
{ id: "local-utility", label: "Utility", icon: "", count: 30
## },
## ],
## },
## ];

##  CONTOH IMPLEMENTASI TOOLS LOCAL PENTING
WordCounter.tsx — Real-time counter
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
paragraphs: text === "" ? 0 :
text.split(/\n\s*\n/).filter(Boolean).length,
lines: text === "" ? 0 : text.split("\n").length,
readingTime:
Math.ceil(text.trim().split(/\s+/).filter(Boolean).length / 200),
uniqueWords: new Set(text.toLowerCase().match(/\b\w+\b/g) ||
## []).size,
## };

return (
<div className="max-w-3xl mx-auto space-y-4">
<div className="flex items-start justify-between">
## <div>
<h2 className="text-2xl font-bold text-white">Penghitung
## Kata</h2>
<p className="text-gray-400 text-sm mt-1">Hitung kata,
karakter, kalimat, paragraf secara real-time</p>
## </div>
<ToolBadge type="local" />
## </div>

<Textarea
value={text}
onChange={(e) => setText(e.target.value)}
placeholder="Ketik atau paste teks di sini..."
rows={8}
className="w-full"
## />

<div className="grid grid-cols-2 sm:grid-cols-4 gap-3">
## {[
{ label: "Kata", value: stats.words },
{ label: "Karakter", value: stats.characters },
{ label: "Tanpa Spasi", value: stats.charactersNoSpace },
{ label: "Kalimat", value: stats.sentences },
{ label: "Paragraf", value: stats.paragraphs },
{ label: "Baris", value: stats.lines },

{ label: "Kata Unik", value: stats.uniqueWords },
{ label: "Baca (mnt)", value: stats.readingTime },
## ].map((stat) => (
<Card key={stat.label} className="text-center p-3">
<div className="text-2xl font-bold
text-violet-400">{stat.value.toLocaleString()}</div>
<div className="text-gray-400 text-xs
mt-1">{stat.label}</div>
</Card>
## ))}
## </div>
## </div>
## );
## }

PasswordGenerator.tsx — Generator password kuat
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
## };

export default function PasswordGenerator() {
const [length, setLength] = useState(16);
const [options, setOptions] = useState({
uppercase: true, lowercase: true, numbers: true, symbols: true,
## });
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

## Array.from(
{ length },
() => charset[Math.floor(Math.random() * charset.length)]
## ).join("")
## );
setPasswords(newPasswords);
}, [length, options, count]);

const getStrength = (len: number, optCount: number) => {
const score = len * optCount;
if (score < 32) return { label: "Lemah", color: "text-red-400" };
if (score < 64) return { label: "Sedang", color: "text-yellow-400"
## };
if (score < 96) return { label: "Kuat", color: "text-blue-400" };
return { label: "Sangat Kuat", color: "text-green-400" };
## };

const activeOptions = Object.values(options).filter(Boolean).length;
const strength = getStrength(length, activeOptions);

return (
<div className="max-w-2xl mx-auto space-y-4">
<div className="flex items-start justify-between">
## <div>
<h2 className="text-2xl font-bold text-white">Generator
## Password</h2>
<p className="text-gray-400 text-sm mt-1">Generate password
kuat dengan aturan kustom — offline</p>
## </div>
<ToolBadge type="local" />
## </div>

<Card className="space-y-4">
{/* Length slider */}
## <div>
<div className="flex justify-between mb-1">
<label className="text-gray-300 text-sm">Panjang: <span
className="text-violet-400 font-bold">{length}</span></label>
<span className={`text-sm font-medium
## ${strength.color}`}>{strength.label}</span>
## </div>
## <input
type="range" min={6} max={128} value={length}
onChange={(e) => setLength(Number(e.target.value))}
className="w-full accent-violet-500"
## />
## </div>


## {/* Options */}
<div className="grid grid-cols-2 gap-2">
{(Object.keys(options) as (keyof typeof
options)[]).map((key) => (
<label key={key} className="flex items-center gap-2
cursor-pointer">
## <input
type="checkbox"
checked={options[key]}
onChange={() => setOptions((prev) => ({ ...prev,
## [key]: !prev[key] }))}
className="accent-violet-500 w-4 h-4"
## />
<span className="text-gray-300 text-sm capitalize">
{key === "uppercase" ? "HURUF BESAR" : key ===
"lowercase" ? "huruf kecil" : key === "numbers" ? "Angka 0-9" :
"Simbol !@#$"}
## </span>
## </label>
## ))}
## </div>

## {/* Count */}
<div className="flex items-center gap-3">
<label className="text-gray-300 text-sm">Jumlah:</label>
## <input
type="number" min={1} max={20} value={count}
onChange={(e) => setCount(Math.min(20, Math.max(1,
## Number(e.target.value))))}
className="w-20 bg-gray-800 text-white rounded px-2 py-1
text-sm border border-gray-700"
## />
## </div>

<Button onClick={generate} className="w-full"> Generate
Password</Button>
</Card>

## {passwords.length > 0 && (
<Card className="space-y-2">
{passwords.map((pw, i) => (
<div key={i} className="flex items-center justify-between
bg-gray-950 rounded p-2 gap-2">
<code className="text-green-400 font-mono text-sm flex-1
break-all">{pw}</code>
<CopyButton text={pw} />
## </div>
## ))}

</Card>
## )}
## </div>
## );
## }

ColorConverter.tsx — Konverter warna lengkap
import { useState } from "react";
import Card from "../../../components/UI/Card";
import Input from "../../../components/UI/Input";
import CopyButton from "../../../components/UI/CopyButton";
import ToolBadge from "../../../components/UI/ToolBadge";

function hexToRgb(hex: string): [number, number, number] | null {
const result =
## /^#?([a-f\d]{2})([a-f\d]{2})([a-f\d]{2})$/i.exec(hex.trim());
return result ? [parseInt(result[1], 16), parseInt(result[2], 16),
parseInt(result[3], 16)] : null;
## }

function rgbToHsl(r: number, g: number, b: number): [number, number,
number] {
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
## }
## }
return [Math.round(h * 360), Math.round(s * 100), Math.round(l *
## 100)];
## }

function rgbToCmyk(r: number, g: number, b: number): [number, number,
number, number] {
const R = r / 255, G = g / 255, B = b / 255;
const k = 1 - Math.max(R, G, B);
if (k === 1) return [0, 0, 0, 100];
return [
Math.round(((1 - R - k) / (1 - k)) * 100),
Math.round(((1 - G - k) / (1 - k)) * 100),

Math.round(((1 - B - k) / (1 - k)) * 100),
## Math.round(k * 100),
## ];
## }

export default function ColorConverter() {
const [hex, setHex] = useState("#6d28d9");
const rgb = hexToRgb(hex);
const hsl = rgb ? rgbToHsl(...rgb) : null;
const cmyk = rgb ? rgbToCmyk(...rgb) : null;

const outputs = rgb && hsl && cmyk ? [
{ label: "HEX", value: hex.toLowerCase(), copy: hex },
{ label: "RGB", value: `rgb(${rgb[0]}, ${rgb[1]}, ${rgb[2]})`,
copy: `rgb(${rgb[0]}, ${rgb[1]}, ${rgb[2]})` },
{ label: "HSL", value: `hsl(${hsl[0]}, ${hsl[1]}%, ${hsl[2]}%)`,
copy: `hsl(${hsl[0]}, ${hsl[1]}%, ${hsl[2]}%)` },
{ label: "CMYK", value: `cmyk(${cmyk[0]}%, ${cmyk[1]}%,
${cmyk[2]}%, ${cmyk[3]}%)`, copy: `cmyk(${cmyk[0]}%, ${cmyk[1]}%,
## ${cmyk[2]}%, ${cmyk[3]}%)` },
{ label: "CSS Var", value: `--color-accent: ${hex};`, copy:
## `--color-accent: ${hex};` },
{ label: "Tailwind", value: `#${hex.replace("#","")}`, copy: hex
## },
## ] : [];

return (
<div className="max-w-2xl mx-auto space-y-4">
<div className="flex items-start justify-between">
## <div>
<h2 className="text-2xl font-bold text-white">Konverter
## Warna</h2>
<p className="text-gray-400 text-sm mt-1">Konversi HEX ↔ RGB
↔ HSL ↔ CMYK — offline</p>
## </div>
<ToolBadge type="local" />
## </div>

<Card className="flex items-center gap-4">
## <div
className="w-20 h-20 rounded-xl shadow-lg border
border-gray-700 flex-shrink-0 cursor-pointer"
style={{ backgroundColor: rgb ? hex : "#6d28d9" }}
## />
<div className="flex-1">
## <input
type="color"
value={rgb ? hex : "#6d28d9"}

onChange={(e) => setHex(e.target.value)}
className="mb-2 w-full h-8 rounded cursor-pointer
bg-transparent"
## />
<Input
value={hex}
onChange={(e) => setHex(e.target.value)}
placeholder="#6d28d9"
className="font-mono"
## />
## </div>
</Card>

## {outputs.length > 0 && (
<div className="grid gap-2">
## {outputs.map((out) => (
<Card key={out.label} className="flex items-center
justify-between py-2">
<span className="text-gray-500 text-xs
w-16">{out.label}</span>
<code className="text-green-400 font-mono text-sm flex-1
mx-3">{out.value}</code>
<CopyButton text={out.copy} />
</Card>
## ))}
## </div>
## )}
## </div>
## );
## }

##  INSTRUKSI IMPLEMENTASI AKHIR
## WAJIB DILAKUKAN:
- Buat semua 260 tools local dengan JavaScript murni — tidak ada API call sama sekali
- Setiap tool AI harus menggunakan useAppStore().selectedModel bukan hardcode model
- ModelSelector harus tampil di Header dan selalu visible
- ToolBadge harus tampil di setiap tool (AI atau Local)
- Footer wajib ada "Powered by Puter" link
- Lazy loading semua tools dengan React.lazy() + Suspense untuk performa
- Fuse.js search untuk mencari semua 850+ tools berdasarkan nama, deskripsi, tags
- Puter KV integration untuk tools yang butuh persistensi (notepad, tracker, dll)
## MODELS YANG DIGUNAKAN:

● claude-opus-4-6 — Paling cerdas, untuk tugas kompleks
● claude-sonnet-4-6 — Lebih cepat, untuk tugas sehari-hari
● Default: claude-sonnet-4-6
CARA PANGGIL AI (WAJIB pakai pattern ini):
// Selalu ambil model dari store — JANGAN hardcode!
const { selectedModel } = useAppStore();

## // Non-streaming:
const res = await window.puter.ai.chat(prompt, { model: selectedModel
## });
const text = res.message.content[0].text;

## // Streaming:
const stream = await window.puter.ai.chat(prompt, { model:
selectedModel, stream: true });
for await (const chunk of stream) {
const piece = chunk?.text ?? "";
## }

CARA BUAT TOOLS LOCAL (WAJIB semua mandiri):
// TIDAK BOLEH ADA window.puter.ai.chat() di tools local/
// TIDAK BOLEH ADA fetch() ke external API
// SEMUA logika harus JavaScript browser native
// Boleh menggunakan Web Crypto API, Canvas API, Web Audio API
// Boleh menggunakan CDN library di index.html (qrcode.js, dll)

PRIORITAS BUILD (urutan pengerjaan):
- Setup proyek: package.json, vite.config.ts, tailwind.config.js, tsconfig.json
- index.html (dengan Puter.js script tag)
- src/types/puter.d.ts
- src/store/useAppStore.ts + toolRegistry.ts
- src/lib/puter.ts + utils.ts + localUtils.ts
- src/components/UI/*.tsx (semua 15 komponen)
- src/components/Layout/*.tsx (Header, Sidebar, Footer, ToolContainer)
- src/pages/HomePage.tsx + ToolPage.tsx
- src/App.tsx + src/main.tsx
- Local tools (260 file) — paralel semua subfolder
- AI tools (590+ file) — paralel semua subfolder
## TOTAL FILES:
● Config: 5 file

● Types: 1 file
● Store: 2 file
● Lib: 4 file
● Components UI: 15 file
● Components Layout: 4 file
● Pages: 3 file
● Local Tools: ~260 file
● AI Tools: ~590 file
● TOTAL: ~884 file
## ✅ CHECKLIST SEBELUM SELESAI
● [ ] index.html punya <script src="https://js.puter.com/v2/"></script>
● [ ] ModelSelector ada di Header, bisa switch antara claude-opus-4-6 dan
claude-sonnet-4-6
● [ ] Setiap AI tool pakai selectedModel dari useAppStore (tidak hardcode)
● [ ] Setiap tool punya ToolBadge (AI violet / Local green)
● [ ] Semua 260 local tools berjalan 100% tanpa AI
● [ ] Footer ada "Powered by Puter" link ke https://developer.puter.com
● [ ] Search berfungsi untuk semua 850+ tools
● [ ] Lazy loading tools aktif
● [ ] Sidebar bisa collapse/expand per kategori
● [ ] Tools yang perlu simpan data pakai Puter KV
## MULAI BUILD SEKARANG — SEMUA FILE PARALLEL — NO PLACEHOLDER!



EHOLDER!



