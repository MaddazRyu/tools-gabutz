# ╔══════════════════════════════════════════════════════════════════╗
# ║         PUTERTOOLS - MEGA AI TOOLS PLATFORM                     ║
# ║         Blueprint untuk Replit AI Agent                         ║
# ║         Model: claude-opus-4-7 | Bahasa: Indonesia              ║
# ╚══════════════════════════════════════════════════════════════════╝

# INSTRUKSI UNTUK REPLIT AI AGENT:
# Baca seluruh file ini. Buat SEMUA file yang disebutkan secara parallel.
# Jangan skip satu pun. Setiap file harus fully functional, no placeholders.
# Stack: React + TypeScript (TSX) + Vite + TailwindCSS
# AI Provider: Puter.js (gratis, tanpa API key)
# Model AI WAJIB: claude-opus-4-7 untuk semua fitur AI

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

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
        chat: (prompt: string | object[], options?: { model?: string; stream?: boolean }) => Promise<any>;
        txt2img: (prompt: string, options?: { model?: string }) => Promise<HTMLImageElement>;
        txt2speech: (text: string, options?: { provider?: string }) => Promise<HTMLAudioElement>;
        speech2txt: (file: File, options?: { model?: string }) => Promise<{ text: string }>;
        img2txt: (file: File) => Promise<string>;
        speech2speech: (file: File, options?: object) => Promise<any>;
        txt2vid: (prompt: string, options?: object) => Promise<any>;
      };
      fs: {
        write: (path: string, data: any) => Promise<any>;
        read: (path: string) => Promise<Blob>;
        readdir: (path: string) => Promise<any[]>;
        delete: (path: string) => Promise<void>;
        upload: (file: File, path: string) => Promise<any>;
        getReadURL: (path: string) => Promise<string>;
        mkdir: (path: string) => Promise<void>;
        copy: (src: string, dst: string) => Promise<void>;
        move: (src: string, dst: string) => Promise<void>;
        stat: (path: string) => Promise<any>;
      };
      kv: {
        set: (key: string, value: any) => Promise<void>;
        get: (key: string) => Promise<any>;
        del: (key: string) => Promise<void>;
        list: (pattern: string) => Promise<any[]>;
        flush: () => Promise<void>;
        incr: (key: string, amount?: number) => Promise<number>;
      };
      auth: {
        signIn: () => Promise<void>;
        signOut: () => Promise<void>;
        isSignedIn: () => boolean;
        getUser: () => Promise<{ username: string; uuid: string }>;
        getMonthlyUsage: () => Promise<any>;
      };
      net: {
        fetch: (url: string, options?: RequestInit) => Promise<Response>;
      };
      hosting: {
        create: (subdomain: string, dir: string) => Promise<any>;
        list: () => Promise<any[]>;
        delete: (subdomain: string) => Promise<void>;
      };
    };
  }
}
export {};
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## STRUKTUR FOLDER LENGKAP

```
putertools/
├── index.html
├── package.json
├── vite.config.ts
├── tailwind.config.js
├── tsconfig.json
├── src/
│   ├── main.tsx
│   ├── App.tsx
│   ├── types/
│   │   └── puter.d.ts
│   ├── lib/
│   │   ├── puter.ts          # helper wrapper semua puter functions
│   │   ├── utils.ts          # helper umum
│   │   └── constants.ts      # konstanta global
│   ├── components/
│   │   ├── Layout/
│   │   │   ├── Sidebar.tsx
│   │   │   ├── Header.tsx
│   │   │   └── ToolContainer.tsx
│   │   └── UI/
│   │       ├── Button.tsx
│   │       ├── Input.tsx
│   │       ├── Textarea.tsx
│   │       ├── Card.tsx
│   │       ├── Badge.tsx
│   │       ├── Spinner.tsx
│   │       ├── Toast.tsx
│   │       ├── Modal.tsx
│   │       ├── ProgressBar.tsx
│   │       ├── CopyButton.tsx
│   │       ├── FileUpload.tsx
│   │       └── StreamOutput.tsx
│   ├── tools/
│   │   ├── writing/           # 50+ tools menulis
│   │   ├── content/           # 50+ tools konten kreator
│   │   ├── image/             # 30+ tools gambar
│   │   ├── audio/             # 30+ tools audio
│   │   ├── video/             # 20+ tools video
│   │   ├── developer/         # 60+ tools developer
│   │   ├── seo/               # 40+ tools SEO
│   │   ├── social/            # 50+ tools sosial media
│   │   ├── productivity/      # 50+ tools produktivitas
│   │   ├── education/         # 40+ tools pendidikan
│   │   ├── business/          # 40+ tools bisnis
│   │   ├── data/              # 30+ tools data & analitik
│   │   ├── health/            # 20+ tools kesehatan
│   │   ├── legal/             # 20+ tools hukum
│   │   ├── finance/           # 20+ tools keuangan
│   │   ├── fun/               # 20+ tools hiburan
│   │   └── local/             # 30+ tools offline (tanpa AI)
│   └── store/
│       └── toolStore.ts       # state management navigasi
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## DAFTAR LENGKAP SEMUA TOOLS (600+ fitur)

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
# Catatan: Gunakan puter.ai.txt2img() untuk generate,
# tools editing/analisis pakai claude-opus-4-7 untuk deskripsi/prompt

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
123. ImageAnalyzer.tsx        - Analisis isi gambar (OCR + deskripsi) via img2txt
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
159. ASMR.ScriptWriter.tsx    - Skrip konten ASMR
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
172. B-RollIdeas.tsx          - Ide footage B-roll untuk video
173. VideoTitleABTest.tsx     - A/B test judul video
174. VideoEndScreenScript.tsx - Skrip end screen/outro
175. ViralAnalyzerYoutube.tsx - Analisis potensi viral YouTube (claude-opus-4-7)
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

190. CodeExplainer.tsx        - Jelaskan kode yang membingungkan
191. CodeReviewer.tsx         - Review kode + saran perbaikan
192. CodeDebugger.tsx         - Debug error + solusi
193. CodeConverter.tsx        - Konversi kode antar bahasa
194. CodeOptimizer.tsx        - Optimasi performa kode
195. CodeDocGenerator.tsx     - Buat dokumentasi kode
196. CodeCommentWriter.tsx    - Tambahkan komentar ke kode
197. RegexGenerator.tsx       - Generate regex dari deskripsi
198. SQLQueryWriter.tsx       - Buat query SQL dari bahasa alami
199. SQLOptimizer.tsx         - Optimasi query SQL
200. APIDocWriter.tsx         - Buat dokumentasi API
201. READMEWriter.tsx         - Buat README.md project
202. GitCommitMessage.tsx     - Buat pesan commit Git yang baik
203. GitIgnoreGenerator.tsx   - Buat .gitignore untuk tech stack
204. DockerfileGenerator.tsx  - Buat Dockerfile
205. CICDPipelineWriter.tsx   - Buat config CI/CD
206. EnvFileGenerator.tsx     - Template .env file
207. UnitTestWriter.tsx       - Buat unit test dari kode
208. MockDataGenerator.tsx    - Generate mock/dummy data JSON
209. JSONFormatter.tsx        - Format + validasi JSON
210. JSONtoCSV.tsx            - Konversi JSON ke CSV (lokal)
211. CSVtoJSON.tsx            - Konversi CSV ke JSON (lokal)
212. XMLFormatter.tsx         - Format + validasi XML
213. MarkdownEditor.tsx       - Editor Markdown dengan preview
214. HTMLGenerator.tsx        - Buat HTML dari deskripsi
215. CSSGenerator.tsx         - Buat CSS dari deskripsi desain
216. TailwindConverter.tsx    - Konversi CSS biasa ke Tailwind
217. JSFunctionWriter.tsx     - Buat fungsi JavaScript
218. PythonFunctionWriter.tsx - Buat fungsi Python
219. AlgorithmExplainer.tsx   - Jelaskan algoritma
220. DataStructureExplainer.tsx- Jelaskan struktur data
221. DesignPatternAdvisor.tsx - Rekomendasi design pattern
222. ArchitectureAdvisor.tsx  - Rekomendasi arsitektur sistem
223. SecurityChecker.tsx      - Cek kerentanan keamanan kode
224. PerformanceTips.tsx      - Tips optimasi performa web
225. AccessibilityChecker.tsx - Cek aksesibilitas UI dari deskripsi
226. SEOTechAudit.tsx         - Audit teknis SEO
227. PWAChecklist.tsx         - Checklist Progressive Web App
228. APIEndpointDesigner.tsx  - Desain endpoint API RESTful
229. DatabaseSchemaDesigner.tsx- Desain skema database
230. ERDiagramTextCreator.tsx - Buat ER diagram dalam teks
231. SystemDesignHelper.tsx   - Bantu desain sistem skala besar
232. TechStackAdvisor.tsx     - Rekomendasi tech stack untuk proyek
233. DependencyAnalyzer.tsx   - Analisis package.json
234. ErrorMessageExplainer.tsx- Jelaskan error message
235. LogAnalyzer.tsx          - Analisis log aplikasi
236. CodeSnippetLibrary.tsx   - Koleksi snippet code berguna
237. TerminalCommandHelper.tsx- Buat perintah terminal/bash
238. LinuxCommandExplainer.tsx- Jelaskan perintah Linux
239. CronJobGenerator.tsx     - Buat ekspresi cron job
240. WebhookHelper.tsx        - Buat handler webhook
241. GraphQLHelper.tsx        - Buat query/mutation GraphQL
242. SocketIOHelper.tsx       - Kode Socket.io dasar
243. LocalStorageHelper.tsx   - Manajemen localStorage (lokal, tanpa AI)
244. CookieManager.tsx        - Manajemen cookie (lokal)
245. ColorCodeConverter.tsx   - Konversi HEX/RGB/HSL (lokal)
246. Base64Tool.tsx           - Encode/decode Base64 (lokal)
247. HashGenerator.tsx        - Generate hash MD5/SHA (lokal, pakai crypto)
248. URLEncoder.tsx           - Encode/decode URL (lokal)
249. JWTDecoder.tsx           - Decode JWT token (lokal)
250. TimestampConverter.tsx   - Konversi Unix timestamp (lokal)
251. UUIDGenerator.tsx        - Generate UUID (lokal)

### ══════════════════════════════════
### KATEGORI 7: 🔍 TOOLS SEO (42 tools)
### ══════════════════════════════════
# File: src/tools/seo/

252. KeywordResearch.tsx      - Riset keyword dari topik
253. KeywordCluster.tsx       - Kelompokkan keyword serupa
254. LongTailKeyword.tsx      - Temukan keyword long-tail
255. KeywordDifficulty.tsx    - Estimasi kesulitan keyword
256. SearchIntentAnalyzer.tsx - Analisis intent keyword
257. LSIKeywordGenerator.tsx  - Generator keyword LSI
258. KeywordGapAnalysis.tsx   - Analisis gap keyword vs kompetitor
259. TitleTagOptimizer.tsx    - Optimasi title tag halaman
260. MetaDescOptimizer.tsx    - Optimasi meta deskripsi
261. URLSlugGenerator.tsx     - Buat URL slug SEO-friendly
262. HeaderStructurePlanner.tsx- Rencana struktur H1/H2/H3
263. ContentBriefWriter.tsx   - Buat content brief untuk penulis
264. SEOContentOutline.tsx    - Outline konten SEO
265. FeaturedSnippetOptimizer.tsx- Optimasi untuk featured snippet
266. SchemaMarkupGenerator.tsx- Buat schema markup JSON-LD
267. FAQSchemaWriter.tsx      - Buat FAQ schema markup
268. BreadcrumbSchema.tsx     - Buat breadcrumb schema
269. LocalSEOOptimizer.tsx    - Optimasi SEO lokal
270. GBPDescWriter.tsx        - Deskripsi Google Business Profile
271. BacklinkOutreachEmail.tsx - Email outreach backlink
272. GuestPostPitch.tsx       - Pitch artikel tamu
273. InternalLinkingStrategy.tsx- Strategi internal linking
274. AnchorTextGenerator.tsx  - Generator anchor text natural
275. CompetitorContentGap.tsx - Analisis gap konten vs kompetitor
276. TopicClusterPlanner.tsx  - Rencanakan topic cluster
277. PillarPageOutline.tsx    - Outline halaman pilar
278. ContentAuditHelper.tsx   - Panduan audit konten lama
279. RedirectMapper.tsx       - Rencana redirect 301
280. SitemapPlanner.tsx       - Rencana struktur sitemap
281. RobotstxtGenerator.tsx   - Buat robots.txt
282. HreflangHelper.tsx       - Buat tag hreflang
283. PageSpeedTips.tsx        - Tips optimasi PageSpeed
284. CoreWebVitals.tsx        - Penjelasan dan tips Core Web Vitals
285. E-E-A-TChecker.tsx       - Audit E-E-A-T konten
286. SEOAuditChecklist.tsx    - Checklist audit SEO lengkap
287. LocalCitationTemplate.tsx- Template NAP citations
288. GoogleAdsKeyword.tsx     - Riset keyword Google Ads
289. AdCopyWriter.tsx         - Buat teks iklan Google/Meta Ads
290. ABTestHeadline.tsx       - A/B test headline iklan
291. LandingSEOAudit.tsx      - Audit SEO landing page
292. EcomSEOOptimizer.tsx     - Optimasi SEO e-commerce
293. BlogSEOOptimizer.tsx     - Optimasi SEO artikel blog

### ══════════════════════════════════
### KATEGORI 8: 📱 TOOLS SOSIAL MEDIA (48 tools)
### ══════════════════════════════════
# File: src/tools/social/

294. SocialMediaScheduler.tsx - Buat jadwal posting mingguan
295. ContentMixStrategy.tsx   - Strategi mix konten 80/20
296. EngagementBooster.tsx    - Tips tingkatkan engagement
297. CommunityReplyWriter.tsx - Buat balasan komentar komunitas
298. DM.TemplateWriter.tsx    - Template DM/pesan pribadi
299. CrisisResponseWriter.tsx - Tangani krisis di sosmed
300. BrandVoiceGuide.tsx      - Buat panduan brand voice
301. SocialMediaBio.tsx       - Buat bio untuk semua platform
302. ProfileOptimizer.tsx     - Optimasi profil sosmed
303. HashtagStrategy.tsx      - Strategi hashtag per platform
304. HashtagGrouper.tsx       - Kelompokkan hashtag per niche
305. TrendHijacker.tsx        - Manfaatkan tren untuk konten
306. ViralPostFormula.tsx     - Formula postingan viral
307. StoryIdeas.tsx           - Ide konten Instagram/Facebook Story
308. PollCreator.tsx          - Buat konten polling interaktif
309. QuizCreator.tsx          - Buat kuis untuk engagement
310. GiveawayRules.tsx        - Buat aturan giveaway resmi
311. CollabPitch.tsx          - Pitch kolaborasi ke kreator lain
312. SponsorPitch.tsx         - Pitch ke sponsor/brand
313. MediaKit.tsx             - Buat media kit konten kreator
314. PricingCard.tsx          - Buat rate card endorsement
315. InfluencerBrief.tsx      - Brief untuk influencer
316. UGCCampaign.tsx          - Buat kampanye user-generated content
317. ViralChallenge.tsx       - Buat challenge viral
318. CountdownPost.tsx        - Konten countdown event
319. LaunchPost.tsx           - Konten peluncuran produk
320. AnniversaryPost.tsx      - Konten ulang tahun brand
321. MotivationalMonday.tsx   - Konten Motivational Monday
322. TestimonialPost.tsx      - Konten testimonial customer
323. EmployeeSpotlight.tsx    - Konten sorotan karyawan
324. BehindTheScenes.tsx      - Konten behind the scenes
325. ProductLaunchPlan.tsx    - Rencana konten launch produk
326. MemorialDayPost.tsx      - Konten hari besar nasional
327. SeasonalContent.tsx      - Konten musiman/hari raya
328. EngagementQuestion.tsx   - Pertanyaan yang memancing engage
329. SocialListeningReport.tsx- Template laporan social listening
330. CompetitorSocialAudit.tsx- Audit sosmed kompetitor
331. GrowthHackingTips.tsx    - Tips growth hacking sosmed
332. CrossPlatformStrategy.tsx- Strategi cross-platform
333. VideoShortStrategy.tsx   - Strategi konten video pendek
334. PodcastGrowthPlan.tsx    - Rencana pertumbuhan podcast
335. NewsletterGrowth.tsx     - Strategi tumbuhkan subscriber
336. CommunityBuilding.tsx    - Panduan bangun komunitas online
337. SocialAuditReport.tsx    - Laporan audit akun sosmed
338. ROI.Calculator.tsx       - Kalkulasi ROI sosmed (lokal)
339. FollowerAnalysis.tsx     - Analisis tipe follower
340. PostTimingAdvisor.tsx    - Rekomendasi waktu posting
341. EngagementRateCalc.tsx   - Kalkulator engagement rate (lokal)

### ══════════════════════════════════
### KATEGORI 9: ⚡ TOOLS PRODUKTIVITAS (50 tools)
### ══════════════════════════════════
# File: src/tools/productivity/

342. TaskBreakdown.tsx        - Pecah proyek besar jadi tugas kecil
343. PriorityMatrix.tsx       - Buat matriks prioritas Eisenhower
344. GoalSetter.tsx           - Buat SMART goals
345. OKRWriter.tsx            - Buat OKR (Objectives & Key Results)
346. ProjectPlan.tsx          - Buat rencana proyek
347. MeetingAgenda.tsx        - Buat agenda meeting
348. MeetingSummary.tsx       - Ringkas notulen meeting
349. ActionItems.tsx          - Ekstrak action items dari teks
350. DecisionMatrix.tsx       - Buat matriks keputusan
351. ProsConsAnalyzer.tsx     - Analisis pro dan kontra
352. SWOT.Analyzer.tsx        - Analisis SWOT dari deskripsi bisnis
353. BrainstormHelper.tsx     - Fasilitasi sesi brainstorming
354. MindMapCreator.tsx       - Buat mind map teks
355. ProcessMapper.tsx        - Buat peta proses/alur kerja
356. SOPWriter.tsx            - Buat Standard Operating Procedure
357. ChecklistCreator.tsx     - Buat checklist dari proses
358. TimerPlanner.tsx         - Jadwal kerja Pomodoro (lokal)
359. HabitTracker.tsx         - Tracker kebiasaan harian (lokal + KV)
360. JournalPrompts.tsx       - Prompt jurnal harian
361. DailyPlanner.tsx         - Buat rencana harian terstruktur
362. WeeklyReview.tsx         - Template review mingguan
363. MonthlyReview.tsx        - Template review bulanan
364. YearlyGoalPlanner.tsx    - Rencana tujuan tahunan
365. PersonalMission.tsx      - Buat pernyataan misi pribadi
366. TimeAudit.tsx            - Audit penggunaan waktu
367. EnergyMapper.tsx         - Peta energi produktivitas harian
368. FocusBooster.tsx         - Tips meningkatkan fokus
369. DistractionBlocker.tsx   - Rencana blokir distraksi
370. DeepWorkSchedule.tsx     - Jadwal deep work
371. EmailInboxZero.tsx       - Strategi inbox zero
372. FileNamingSystem.tsx     - Sistem penamaan file
373. FolderStructure.tsx      - Buat struktur folder yang rapi
374. NoteOrganizer.tsx        - Sistem organisasi catatan
375. ReadingList.tsx          - Buat daftar baca terstruktur
376. BookSummary.tsx          - Ringkas buku dari judul/deskripsi
377. ArticleSummarizer.tsx    - Ringkas artikel dari paste teks
378. DocumentSummarizer.tsx   - Ringkas dokumen panjang
379. ReportSummarizer.tsx     - Ringkas laporan
380. PresentationOutline.tsx  - Buat outline presentasi
381. PresentationScript.tsx   - Skrip presentasi slide per slide
382. PitchDeckOutline.tsx     - Outline pitch deck startup
383. Speechwriter.tsx         - Buat naskah pidato
384. TalkingPoints.tsx        - Buat talking points untuk presentasi
385. NegotiationScript.tsx    - Skrip negosiasi
386. ConflictResolution.tsx   - Panduan resolusi konflik
387. FeedbackScript.tsx       - Skrip memberikan feedback konstruktif
388. DelegationGuide.tsx      - Panduan delegasi tugas
389. OnboardingPlan.tsx       - Rencana onboarding karyawan baru
390. TrainingPlan.tsx         - Rencana pelatihan
391. KPIBuilder.tsx           - Buat KPI untuk departemen/individu

### ══════════════════════════════════
### KATEGORI 10: 📚 TOOLS PENDIDIKAN (40 tools)
### ══════════════════════════════════
# File: src/tools/education/

392. ExplainLikeFive.tsx      - Jelaskan topik kompleks dengan mudah
393. ConceptExplainer.tsx     - Jelaskan konsep ilmiah
394. HistoryStoryteller.tsx   - Ceritakan sejarah dengan menarik
395. MathSolver.tsx           - Bantu selesaikan soal matematika
396. PhysicsSolver.tsx        - Bantu fisika dengan penjelasan
397. ChemistrySolver.tsx      - Bantu kimia dengan penjelasan
398. BiologyExplainer.tsx     - Jelaskan biologi
399. GeographyHelper.tsx      - Helper geografi
400. QuizGenerator.tsx        - Buat kuis dari materi
401. FlashcardCreator.tsx     - Buat flashcard belajar
402. StudyGuideWriter.tsx     - Buat panduan belajar
403. EssayOutline.tsx         - Outline esai akademik
404. ThesisStatement.tsx      - Buat thesis statement
405. CitationFormatter.tsx    - Format sitasi (APA/MLA/Chicago)
406. LiteratureReview.tsx     - Panduan menulis tinjauan pustaka
407. ResearchQuestions.tsx    - Buat pertanyaan penelitian
408. MethodologyHelper.tsx    - Panduan metodologi penelitian
409. AbstractWriter.tsx       - Buat abstrak penelitian
410. DebateArguments.tsx      - Argumen untuk debat
411. CriticalThinkingHelper.tsx- Pertanyaan berpikir kritis
412. AnalogiesGenerator.tsx   - Buat analogi untuk pemahaman
413. MemoryTechniques.tsx     - Teknik menghafal (mnemonik)
414. LearningPathCreator.tsx  - Buat jalur belajar mandiri
415. CourseOutlineWriter.tsx  - Buat outline kursus online
416. LessonPlanWriter.tsx     - Buat rencana pelajaran (RPP)
417. AssignmentCreator.tsx    - Buat tugas/assignment
418. RubricCreator.tsx        - Buat rubrik penilaian
419. FeedbackOnEssay.tsx      - Feedback pada esai siswa
420. TranslateAndExplain.tsx  - Terjemah + penjelasan kosakata
421. GrammarLesson.tsx        - Pelajaran tata bahasa
422. VocabularyBuilder.tsx    - Builder kosakata bahasa asing
423. PronunciationGuide.tsx   - Panduan pengucapan
424. LanguageLearningPlan.tsx - Rencana belajar bahasa
425. IELTSEssayHelper.tsx     - Bantuan esai IELTS/TOEFL
426. CodingTutor.tsx          - Tutor coding untuk pemula
427. ScienceProjectIdeas.tsx  - Ide proyek sains
428. BookReport.tsx           - Buat book report
429. PresentationFeedback.tsx - Feedback presentasi
430. MockInterview.tsx        - Simulasi wawancara kerja
431. ScholarshipEssay.tsx     - Esai beasiswa

### ══════════════════════════════════
### KATEGORI 11: 💼 TOOLS BISNIS (42 tools)
### ══════════════════════════════════
# File: src/tools/business/

432. BusinessIdeaGenerator.tsx- Generator ide bisnis
433. BusinessPlanWriter.tsx   - Buat business plan
434. ExecutiveSummary.tsx     - Buat executive summary
435. MarketResearch.tsx       - Riset pasar dari niche
436. TAMCalculator.tsx        - Hitung TAM/SAM/SOM
437. CompetitorMatrix.tsx     - Matriks perbandingan kompetitor
438. ValueProposition.tsx     - Buat value proposition
439. USPFinder.tsx            - Temukan Unique Selling Proposition
440. PricingStrategy.tsx      - Strategi penetapan harga
441. PricingTable.tsx         - Buat tabel paket harga
442. RevenueModel.tsx         - Buat model pendapatan
443. BusinessModelCanvas.tsx  - Isi Business Model Canvas
444. CustomerJourneyMap.tsx   - Buat peta perjalanan customer
445. PainPointAnalyzer.tsx    - Analisis pain point pelanggan
446. SolutionFitChecker.tsx   - Cek problem-solution fit
447. ProductMarketFit.tsx     - Evaluasi product-market fit
448. GTMStrategy.tsx          - Strategi go-to-market
449. LaunchChecklist.tsx      - Checklist peluncuran produk/bisnis
450. InvestorPitch.tsx        - Buat pitch ke investor
451. FundingProposal.tsx      - Proposal pendanaan
452. GrantApplicationHelper.tsx- Bantu proposal hibah
453. PartnershipProposal.tsx  - Proposal kemitraan bisnis
454. MOUDraft.tsx             - Draft Memorandum of Understanding
455. ContractTemplate.tsx     - Template kontrak dasar
456. InvoiceTemplate.tsx      - Template faktur (lokal)
457. QuotationTemplate.tsx    - Template penawaran harga
458. ProjectProposal.tsx      - Proposal proyek ke klien
459. CaseStudyTemplate.tsx    - Template studi kasus pelanggan
460. CustomerFeedbackAnalysis.tsx- Analisis feedback pelanggan
461. NPSAnalyzer.tsx          - Analisis Net Promoter Score
462. SupportTicketResponse.tsx- Buat respons tiket support
463. RefundEmailWriter.tsx    - Email kebijakan refund
464. TermsOfService.tsx       - Draft Syarat & Ketentuan
465. PrivacyPolicy.tsx        - Draft Kebijakan Privasi
466. HR.JobPostingWriter.tsx  - Buat posting lowongan kerja
467. InterviewQuestions.tsx   - Buat pertanyaan wawancara HRD
468. OfferLetterWriter.tsx    - Buat surat penawaran kerja
469. TerminationLetter.tsx    - Surat pemutusan hubungan kerja
470. WarningLetter.tsx        - Surat peringatan karyawan
471. CompanyAnnouncement.tsx  - Pengumuman internal perusahaan
472. BudgetTemplate.tsx       - Template anggaran (lokal)
473. ROICalculator.tsx        - Kalkulasi ROI proyek (lokal)

### ══════════════════════════════════
### KATEGORI 12: 📊 TOOLS DATA & ANALITIK (30 tools)
### ══════════════════════════════════
# File: src/tools/data/

474. DataInterpreter.tsx      - Interpretasi data/angka dari paste
475. ChartDescriber.tsx       - Deskripsikan data untuk chart
476. SurveyAnalyzer.tsx       - Analisis hasil survei
477. StatisticsExplainer.tsx  - Jelaskan statistik
478. TrendAnalyzer.tsx        - Analisis tren dari data
479. AnomalyDetector.tsx      - Deteksi anomali dari data paste
480. CorrelationFinder.tsx    - Temukan korelasi dalam data
481. DataCleaner.tsx          - Panduan bersihkan data kotor
482. DataStoryTeller.tsx      - Ubah data jadi narasi
483. ExecutiveReport.tsx      - Buat laporan eksekutif dari data
484. KPIDashboard.tsx         - Buat template KPI dashboard
485. MetricsDefinition.tsx    - Definisikan metrik bisnis
486. FunnelAnalysis.tsx       - Analisis funnel konversi
487. CohortAnalysis.tsx       - Jelaskan cohort analysis
488. AttributionModeling.tsx  - Model atribusi marketing
489. CustomerSegmentation.tsx - Segmentasi pelanggan
490. RFMAnalysis.tsx          - Analisis RFM pelanggan
491. ChurnPrediction.tsx      - Prediksi churn pelanggan
492. LTV.Calculator.tsx       - Hitung Customer Lifetime Value (lokal)
493. CAC.Calculator.tsx       - Hitung Customer Acquisition Cost (lokal)
494. BreakevenCalculator.tsx  - Kalkulasi break-even point (lokal)
495. FinancialRatioCalc.tsx   - Kalkulator rasio keuangan (lokal)
496. PivotTableHelper.tsx     - Bantu membuat pivot table
497. DashboardDesignTips.tsx  - Tips desain dashboard
498. DataVisualizationAdvisor.tsx- Pilih jenis chart yang tepat
499. ABTestCalculator.tsx     - Kalkulasi statistik A/B test (lokal)
500. SampleSizeCalc.tsx       - Hitung ukuran sampel (lokal)
501. HypothesisTester.tsx     - Buat hipotesis penelitian
502. DataETL.Explainer.tsx    - Jelaskan proses ETL
503. BigDataConcepts.tsx      - Jelaskan konsep big data

### ══════════════════════════════════
### KATEGORI 13: 🏥 TOOLS KESEHATAN (20 tools)
### ══════════════════════════════════
# File: src/tools/health/
# DISCLAIMER: Selalu tampilkan "Bukan pengganti dokter"

504. SymptomChecker.tsx       - Cek gejala + rekomendasi (dengan disclaimer)
505. MedicationReminder.tsx   - Buat jadwal minum obat
506. NutritionAnalyzer.tsx    - Analisis kandungan gizi makanan
507. MealPlanGenerator.tsx    - Buat rencana makan sehat
508. WorkoutPlanGenerator.tsx - Buat rencana olahraga
509. BMI.Calculator.tsx       - Kalkulator BMI (lokal)
510. CalorieCalculator.tsx    - Kalkulator kalori harian (lokal)
511. WaterIntakeCalc.tsx      - Kebutuhan air harian (lokal)
512. SleepScheduler.tsx       - Jadwal tidur optimal
513. StressReliefTips.tsx     - Tips manajemen stres
514. MeditationScript.tsx     - Skrip meditasi terpandu
515. MentalHealthJournal.tsx  - Prompt jurnal kesehatan mental
516. AnxietyReliefTips.tsx    - Tips redakan kecemasan
517. FirstAidGuide.tsx        - Panduan pertolongan pertama
518. VaccineSchedule.tsx      - Jadwal vaksinasi (info umum)
519. PregnancyInfo.tsx        - Info kehamilan (dengan disclaimer)
520. BabyDevMilestones.tsx    - Milestone perkembangan bayi
521. FitnessGoalSetter.tsx    - Buat target kebugaran
522. RecoveryPlan.tsx         - Rencana pemulihan cedera
523. HealthChecklistYearly.tsx- Checklist kesehatan tahunan

### ══════════════════════════════════
### KATEGORI 14: ⚖️ TOOLS HUKUM (20 tools)
### ══════════════════════════════════
# File: src/tools/legal/
# DISCLAIMER: Selalu tampilkan "Bukan pengganti advokat"

524. ContractAnalyzer.tsx     - Analisis kontrak + risiko
525. LegalTermExplainer.tsx   - Jelaskan istilah hukum
526. NDAdraft.tsx             - Draft Non-Disclosure Agreement
527. FreelanceContract.tsx    - Kontrak freelancer
528. RentalAgreement.tsx      - Perjanjian sewa-menyewa
529. EmploymentContract.tsx   - Kontrak kerja dasar
530. ServiceAgreement.tsx     - Perjanjian layanan
531. DisputeLetterWriter.tsx  - Surat sengketa/keberatan
532. ConsumerRightsGuide.tsx  - Panduan hak konsumen Indonesia
533. IP.ProtectionGuide.tsx   - Panduan perlindungan HKI
534. CopyrightGuide.tsx       - Panduan hak cipta
535. TrademarkSearch.tsx      - Panduan cari merek dagang
536. StartupLegalChecklist.tsx- Checklist legal startup
537. PTFoundingGuide.tsx      - Panduan pendirian PT Indonesia
538. UMKMLegalGuide.tsx       - Panduan legal UMKM Indonesia
539. TaxObligationGuide.tsx   - Panduan kewajiban pajak (info umum)
540. LaborLawSummary.tsx      - Ringkasan UU Ketenagakerjaan
541. DataPrivacyCompliance.tsx- Panduan kepatuhan privasi data
542. EcommerceRegulation.tsx  - Regulasi e-commerce Indonesia
543. CyberCrimeLaw.tsx        - Info hukum kejahatan siber Indonesia

### ══════════════════════════════════
### KATEGORI 15: 💰 TOOLS KEUANGAN (22 tools)
### ══════════════════════════════════
# File: src/tools/finance/
# DISCLAIMER: Bukan saran investasi

544. BudgetPlanner.tsx        - Buat anggaran bulanan (lokal + KV)
545. SavingsCalculator.tsx    - Kalkulator tabungan (lokal)
546. LoanCalculator.tsx       - Kalkulator cicilan KPR/KTA (lokal)
547. InvestmentCalculator.tsx - Kalkulator investasi compound (lokal)
548. RetirementPlanner.tsx    - Planner dana pensiun (lokal)
549. EmergencyFund.tsx        - Hitung dana darurat (lokal)
550. DebtPayoffPlanner.tsx    - Rencana pelunasan hutang (lokal)
551. NetWorthCalculator.tsx   - Kalkulator kekayaan bersih (lokal)
552. InvestmentExplainer.tsx  - Jelaskan instrumen investasi
553. StockAnalysisHelper.tsx  - Bantu analisis saham dasar
554. CryptoExplainer.tsx      - Jelaskan cryptocurrency
555. DeFiExplainer.tsx        - Jelaskan DeFi
556. MutualFundExplainer.tsx  - Jelaskan reksa dana
557. InsuranceAdvisor.tsx     - Panduan pilih asuransi
558. TaxPlanning.tsx          - Tips perencanaan pajak
559. FreelanceTaxGuide.tsx    - Panduan pajak freelancer
560. FinancialGoals.tsx       - Buat tujuan keuangan SMART
561. ExpenseTracker.tsx       - Tracker pengeluaran (lokal + KV)
562. FinancialLiteracy.tsx    - Kuis literasi keuangan
563. SideHustleIdeas.tsx      - Ide penghasilan sampingan
564. PassiveIncomeGuide.tsx   - Panduan passive income
565. FinancialPlan.tsx        - Buat rencana keuangan pribadi

### ══════════════════════════════════
### KATEGORI 16: 🎮 TOOLS HIBURAN & FUN (25 tools)
### ══════════════════════════════════
# File: src/tools/fun/

566. StoryGenerator.tsx       - Buat cerita interaktif
567. RPGStoryCreator.tsx      - Buat skenario game RPG
568. JokeGenerator.tsx        - Generator lelucon
569. RiddleCreator.tsx        - Buat teka-teki
570. TriviaQuizMaker.tsx      - Buat kuis trivia
571. WordGameCreator.tsx      - Buat permainan kata
572. ScavengerHuntCreator.tsx - Buat tantangan scavenger hunt
573. IcebreakerQuestions.tsx  - Pertanyaan ice breaker
574. PartyGameIdeas.tsx       - Ide permainan pesta
575. WouldYouRather.tsx       - Generator pertanyaan "Would You Rather"
576. HoroscopeWriter.tsx      - Buat horoskop kreatif
577. FortuneCookie.tsx        - Buat pesan fortune cookie
578. ComicStrip.tsx           - Buat skrip komik strip
579. FanFictionWriter.tsx     - Buat fan fiction
580. WorldBuilding.tsx        - Buat dunia fiksi
581. CharacterCreator.tsx     - Buat karakter fiksi detail
582. DialogueWriter.tsx       - Buat dialog antar karakter
583. DreamInterpreter.tsx     - Interpretasi mimpi (fun, bukan serius)
584. PersonalityAnalyzer.tsx  - Analisis kepribadian dari deskripsi
585. CompatibilityChecker.tsx - Cek kompatibilitas (fun)
586. BucketListCreator.tsx    - Buat bucket list
587. TravelItinerary.tsx      - Buat rencana perjalanan wisata
588. RecipeGenerator.tsx      - Buat resep dari bahan yang ada
589. MovieRecommender.tsx     - Rekomendasi film dari preferensi
590. BookRecommender.tsx      - Rekomendasi buku

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## TEMPLATE KODE WAJIB UNTUK SETIAP TOOL

Setiap file tool TSX harus mengikuti template ini PERSIS:

```typescript
// src/tools/[kategori]/NamaTool.tsx
import { useState } from "react";
import Card from "../../components/UI/Card";
import Button from "../../components/UI/Button";
import Textarea from "../../components/UI/Textarea";
import Input from "../../components/UI/Input";
import StreamOutput from "../../components/UI/StreamOutput";
import CopyButton from "../../components/UI/CopyButton";
import Spinner from "../../components/UI/Spinner";

// PENTING: Ganti deskripsi sesuai tool
const TOOL_NAME = "Nama Tool";
const TOOL_DESC = "Deskripsi singkat apa yang tool ini lakukan";
const DISCLAIMER = ""; // isi jika perlu disclaimer (kesehatan/hukum/keuangan)

export default function NamaTool() {
  // State
  const [input, setInput] = useState("");
  const [output, setOutput] = useState("");
  const [loading, setLoading] = useState(false);
  const [error, setError] = useState("");
  const [streaming, setStreaming] = useState(false);

  const handleGenerate = async () => {
    if (!input.trim()) {
      setError("Isi input terlebih dahulu.");
      return;
    }
    setLoading(true);
    setError("");
    setOutput("");
    setStreaming(true);

    try {
      // Prompt yang spesifik untuk tool ini
      const prompt = `[PROMPT SPESIFIK TOOL INI - dalam Bahasa Indonesia]
      
Input user: ${input}

Berikan output yang berguna, terstruktur, dan langsung to the point.
Gunakan Bahasa Indonesia.`;

      const stream = await window.puter.ai.chat(prompt, {
        model: "claude-opus-4-7",
        stream: true,
      });

      let fullText = "";
      for await (const chunk of stream) {
        const piece = chunk?.text ?? "";
        fullText += piece;
        setOutput(fullText);
      }
    } catch (err: unknown) {
      const msg = err instanceof Error ? err.message : String(err);
      setError("Error: " + msg);
    } finally {
      setLoading(false);
      setStreaming(false);
    }
  };

  return (
    <div className="max-w-3xl mx-auto space-y-4">
      {/* Header */}
      <div>
        <h2 className="text-2xl font-bold text-white">{TOOL_NAME}</h2>
        <p className="text-gray-400 mt-1">{TOOL_DESC}</p>
        {DISCLAIMER && (
          <p className="text-yellow-500 text-sm mt-2 p-2 bg-yellow-500/10 rounded">
            ⚠️ {DISCLAIMER}
          </p>
        )}
      </div>

      {/* Input */}
      <Card>
        <Textarea
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="Masukkan input di sini..."
          rows={4}
          disabled={loading}
        />
        {error && <p className="text-red-400 text-sm mt-2">{error}</p>}
        <Button
          onClick={handleGenerate}
          disabled={loading || !input.trim()}
          className="mt-3 w-full"
        >
          {loading ? <Spinner /> : "✨ Generate"}
        </Button>
      </Card>

      {/* Output */}
      {output && (
        <Card>
          <div className="flex justify-between items-center mb-2">
            <span className="text-gray-400 text-sm">Hasil:</span>
            <CopyButton text={output} />
          </div>
          <StreamOutput text={output} streaming={streaming} />
        </Card>
      )}
    </div>
  );
}
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## KODE CORE FILES

### package.json:
```json
{
  "name": "putertools",
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
    "lucide-react": "^0.400.0"
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

### vite.config.ts:
```typescript
import { defineConfig } from 'vite';
import react from '@vitejs/plugin-react';

export default defineConfig({
  plugins: [react()],
  server: { port: 3000 }
});
```

### index.html:
```html
<!DOCTYPE html>
<html lang="id">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>PuterTools - 600+ AI Tools Gratis</title>
  <!-- WAJIB: Puter.js -->
  <script src="https://js.puter.com/v2/"></script>
</head>
<body class="bg-gray-950">
  <div id="root"></div>
  <script type="module" src="/src/main.tsx"></script>
</body>
</html>
```

### src/lib/puter.ts (wrapper helper):
```typescript
// Helper functions untuk semua interaksi Puter.js
// Sehingga setiap tool tidak perlu akses window.puter langsung

export async function aiChat(prompt: string): Promise<string> {
  const res = await window.puter.ai.chat(prompt, { model: "claude-opus-4-7" });
  return res.message.content[0].text;
}

export async function* aiStream(prompt: string): AsyncGenerator<string> {
  const stream = await window.puter.ai.chat(prompt, {
    model: "claude-opus-4-7",
    stream: true,
  });
  for await (const chunk of stream) {
    yield chunk?.text ?? "";
  }
}

export async function generateImage(prompt: string): Promise<HTMLImageElement> {
  return window.puter.ai.txt2img(prompt, { model: "gpt-image-2" });
}

export async function textToSpeech(text: string): Promise<HTMLAudioElement> {
  return window.puter.ai.txt2speech(text, { provider: "openai" });
}

export async function speechToText(file: File): Promise<string> {
  const result = await window.puter.ai.speech2txt(file);
  return result.text;
}

export async function imageToText(file: File): Promise<string> {
  return window.puter.ai.img2txt(file);
}

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
```

### src/store/toolStore.ts:
```typescript
import { useState, createContext, useContext } from "react";

// Daftar semua kategori dan tools
export const CATEGORIES = [
  {
    id: "writing", icon: "✍️", label: "Menulis",
    tools: [
      { id: "article-writer", label: "Penulis Artikel" },
      { id: "blog-post", label: "Blog Post" },
      // ... semua 52 tools menulis
    ]
  },
  {
    id: "content", icon: "🎬", label: "Konten Kreator",
    tools: [/* 55 tools */]
  },
  // ... semua 16 kategori
];

// Context untuk navigasi active tool
export type ToolStore = {
  activeToolId: string;
  setActiveToolId: (id: string) => void;
  searchQuery: string;
  setSearchQuery: (q: string) => void;
};

export const ToolContext = createContext<ToolStore>({
  activeToolId: "article-writer",
  setActiveToolId: () => {},
  searchQuery: "",
  setSearchQuery: () => {},
});

export const useToolStore = () => useContext(ToolContext);
```

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## SIDEBAR NAVIGATION

Sidebar harus:
1. Menampilkan semua 16 kategori dengan icon
2. Setiap kategori bisa di-collapse/expand
3. Ada search bar di atas untuk cari tool
4. Active tool di-highlight
5. Tampilkan jumlah tools per kategori
6. Sticky di kiri, scrollable

## HEADER

Header harus:
1. Logo "PuterTools" + tagline "600+ AI Tools Gratis"
2. Badge "Powered by Claude Opus 4.7"
3. Link "Powered by Puter" di pojok kanan (WAJIB dari Puter.js docs)
4. Dark mode only

## HALAMAN UTAMA (sebelum pilih tool)

Tampilkan:
1. Hero section: "600+ AI Tools Gratis, Tanpa API Key"
2. Grid 16 kategori dengan icon dan jumlah tools
3. Tools populer (6 tools featured)
4. Search bar besar di tengah

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

## PERINTAH UNTUK REPLIT AI AGENT

BUAT SEMUA FILE INI SECARA PARALLEL:
1. package.json, vite.config.ts, tsconfig.json, tailwind.config.js
2. index.html
3. src/types/puter.d.ts
4. src/lib/puter.ts, src/lib/utils.ts, src/lib/constants.ts
5. src/components/UI/*.tsx (semua 12 komponen UI)
6. src/components/Layout/*.tsx (semua 3 komponen layout)
7. src/store/toolStore.ts
8. src/App.tsx, src/main.tsx
9. src/tools/writing/*.tsx (52 file)
10. src/tools/content/*.tsx (55 file)
11. src/tools/image/*.tsx (32 file)
12. src/tools/audio/*.tsx (28 file)
13. src/tools/video/*.tsx (22 file)
14. src/tools/developer/*.tsx (62 file)
15. src/tools/seo/*.tsx (42 file)
16. src/tools/social/*.tsx (48 file)
17. src/tools/productivity/*.tsx (50 file)
18. src/tools/education/*.tsx (40 file)
19. src/tools/business/*.tsx (42 file)
20. src/tools/data/*.tsx (30 file)
21. src/tools/health/*.tsx (20 file)
22. src/tools/legal/*.tsx (20 file)
23. src/tools/finance/*.tsx (22 file)
24. src/tools/fun/*.tsx (25 file)

TOTAL: ~650+ file
SETIAP file harus FULLY FUNCTIONAL, tidak ada placeholder.
Model AI WAJIB: claude-opus-4-7
Bahasa output AI: Indonesia
Footer WAJIB: "Powered by Puter" link ke https://developer.puter.com
