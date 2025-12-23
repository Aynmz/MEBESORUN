# MEBESORUN — Mevzuat Destekli Soru-Cevap Konsol Uygulaması

Bu proje Milli Eğitim Bakanlığı mevzuatına dayalı soru-cevap (mevzuat robotu) prototipidir. 
Projede PDF'lerden Lucene ile indeksleme yapılıyor, en alakalı sayfa özetleri alınarak LLM'e prompt oluşturuluyor ve cevap üretiliyor.

Önemli Güvenlik Notu
- Hiçbir zaman API anahtarlarını kaynak koduna gömmeyin. Eğer daha önce gömdüyseniz, anahtarı derhal iptal edin (rotate) ve repo geçmişinden silin.

Gereksinimler
- .NET 8 SDK
- NuGet paketleri: Lucene.Net 4.8.0, PdfPig, Newtonsoft.Json (csproj içinde referanslı)
- (Opsiyonel) OpenAI API erişimi veya yerel LLM endpoint

Kurulum & Çalıştırma (yerel geliştirme)
1. Repo klonlama:
   git clone git@github.com:Aynmz/MEBESORUN.git
   cd MEBESORUN

2. Eski gömülü anahtar varsa: derhal iptal edin (OpenAI panelinden) ve geçmiş temizliği uygulayın (git-filter-repo veya BFG). README'nın güvenlik bölümündeki adımları takip edin.

3. Ortam değişkenini ayarlama:
   - Windows (PowerShell): 
     setx OPENAI_API_KEY "sk-..."
     (PowerShell'e yeniden oturum açın)
   - Linux/macOS (bash):
     export OPENAI_API_KEY="sk-..."

   Eğer GitHub Actions kullanacaksanız repository secret olarak `OPENAI_API_KEY` ekleyin.

4. PDF dosyalarını `Data/` klasörüne koyun (ör: yönetmelikler.pdf).
   Proje, exe ile aynı dizinde `Data` klasörünü arar.

5. Derleme:
   dotnet build

6. Çalıştırma:
   dotnet run --project MEBESORUN_PROJE.csproj
   Program açıldıktan sonra:
   - `yenidizinle` komutu ile PDF'leri yeniden dizinleyin
   - Soru girin; sonuçlarda LLM'den cevap alınır.

Geçmişten Anahtar Temizleme (kısa)
- git-filter-repo veya BFG kullanın. (Dikkat: repo tarihçesi yeniden yazılır; ekip üyelerini bilgilendirin.)

Yerel LLM Kullanmak İsterseniz
- Ollama, GPT4All veya llama.cpp gibi çözümlerle local endpoint kullanılabilir.
- Eğer local endpoint OpenAI-uyumlu bir HTTP API sunuyorsa (örn. `http://localhost:11434/v1/chat/completions`) `OPENAI_BASE_URL` ortam değişkeni ile LocalLlmClient yapılandırılabilir.

CI (opsiyonel)
- Basit bir GitHub Actions workflow ile derleme/test ekleyebilirsiniz (örnek `/.github/workflows/ci.yml`).

Yardım / İlerleme
- İsterseniz ben:
  1. Repo için commit dizisini hazırlayıp README/.gitignore/LocalLlmClient değişikliklerini içeren commit mesajı örneği veririm.
  2. Geçmiş temizliği için çalıştırılabilir script (git-filter-repo örneği) oluştururum.
  3. Lokal LLM entegrasyonu için örnek LocalLlmClient (local endpoint veya subprocess) hazırlarım.

Hangi adımı yapmamı istersiniz şimdi?
