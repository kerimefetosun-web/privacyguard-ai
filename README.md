# PrivacyGuard AI

Cloudflare Workers AI destekli, Türkçe dijital gizlilik farkındalığı web uygulaması. React + Vite + Cloudflare Pages Functions.

## Özellikler
- Tarayıcıda e-posta, Türkiye cep telefonu, olası T.C. kimlik numarası, Türkiye IBAN ve olası IPv4 adresi tespiti
- Yerel maskeleme, risk puanı ve kopyalanabilir güvenli metin
- Cloudflare Workers AI üzerinden **yalnızca maskelenmiş metinle** LLM önerileri
- Mobil uyumlu koyu tema

## Yerel geliştirme
```bash
npm install
npm run dev
npm run build
```
`npm run dev` arayüzü çalıştırır; `/api/analyze` Cloudflare Pages Functions olduğundan gerçek AI özelliğini yerelde çalıştırmak için Wrangler Pages geliştirme ortamı ve AI binding gerekir.

## GitHub + Cloudflare Pages
1. Bu dosyaları bir GitHub deposunun **köküne** yükleyin (`functions/api/analyze.js` yolu korunmalı).
2. Cloudflare Dashboard > Workers & Pages > Create > Pages > Connect to Git.
3. Framework: **Vite**; Build command: `npm run build`; Output directory: `dist`.
4. Pages projesinde Settings > Bindings > Add > **Workers AI**, Variable name: `AI`. Production ortamına uygulayın.
5. Yeni deployment başlatın. Önce metin analizini, ardından AI risk yorumunu deneyin.

## Güvenlik ve sınırlar
- Kural tabanlı tespit eksik veya yanlış eşleşebilir; **tam koruma garantisi yoktur**.
- Risk puanı bilimsel/standart bir güvenlik skoru değildir; yalnızca örnek bir gösterge.
- Metin tarayıcıda maskelenir. **AI butonuna basıldığında maskelenmiş metin ve tespit kategorileri Cloudflare sunucusuna gönderilir.** Tespit edilemeyen hassas bilgiler maskelenmiş metinde kalabilir. Gerçek kişisel sırlarınızı, şifrelerinizi veya kimlik bilgilerinizi deneme için kullanmayın.
- Bu uygulama analiz geçmişini kalıcı olarak saklamaz. Cloudflare'ın altyapı logları ve hizmet koşulları ayrıca geçerlidir.
- Model `@cf/meta/llama-3.1-8b-instruct-fp8` olarak ayarlanmıştır; sağlayıcı ileride model erişimini değiştirebilir.

## Final sunumu önerisi
Örnek metni yükle > Gizlilik analizi yap > tespitleri ve maskelenmiş metni göster > AI risk yorumu > güvenli metni kopyala. Sonra `functions/api/analyze.js` dosyasında gerçek LLM çağrısını göster.
