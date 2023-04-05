# OpenWRT'ye Cloudflare Argo Tunnel Kurulum Rehberi!
Bu rehberimiz içeriğinde sizlerle birlikte uygulayacağımız yöntem neticesinde;   
Cloudflared paketinin OpenWRT ile uyumsuz config içeriğinden dolayı başlangıçta açılmaması sorununu çözeceğiz.  
Bu sayede cihazınız yeniden başladığında veya kesinti olduğu zamanlarda da arayüze erişiminiz kaybolmayacak.  
*Rehberimizi kaynak göstererek paylaşmanız, bilgi kaynağının yitirilmemesi üzere önemle rica olunur. 🙏*   

<p align="left">
  <a href="https://discord.gg/k6y5MBKCPW"><img src="https://img.shields.io/badge/Discord - Chat-blue?logo=discord&logoColor=white" /></a>
</p>

<details>
  <summary>İçindekiler</summary>
  <ol>
    <li>
      <a href="#-başlarken">✨ Başlarken</a>
      <ul>
        <li><a href="#-cloudflared-kurulumu">🪄 Cloudflared Kurulumu</a></li>
      </ul>
    </li>
    <li>
      <a href="#-cloudflare-tunnel-oluşturma">🚀 Cloudflare Tunnel Oluşturma</a>
      <ul>
        <li><a href="#-konnektör-kurulumu-install-connector">🌐 Konnektör Kurulumu (Install Connector)</a></li>
        <li><a href="#%EF%B8%8F-tünel-yönlendirme-route-tunnel">⚙️ Tünel Yönlendirme (Route Tunnel)</a></li>
        <li><a href="#-diğer-cihazları-i̇nternete-çıkarma">🔀 Diğer Cihazları İnternete Çıkarma</a></li>
      </ul>
    </li>
    <li><a href="#-hoş-geldin-cloudflare-argo-tunnel">😎 Hoş Geldin Cloudflare Argo Tunnel!</a></li>
    <li><a href="#-özel-teşekkürler">💖 Özel Teşekkürler</a></li>
  </ol>
</details>

# ✨ Başlarken
[Cloudflare](https://dash.cloudflare.com/login)'e kayıt olun. Add Site butonuna tıklayın ve yönlendirmeleri takip ederek alan adınızı Cloudflare'e bağlayın.  
Konfigürasyon dosyasını düzenlemek için WinSCP programı gerekecektir. [Buradaki bağlantı](https://winscp.net/eng/download.php) üzerinden indirebilirsiniz.  
Aktivasyon için SSH bağlantısı gerekecektir, komut istemi veya WinSCP ile bağlanabilirsiniz. **`Komutlar > PuTTY ile aç`**  
Konfigürasyon dosyasının içeriğini güncellemek için ihtiyacınız olacak dosyaya [buraya tıklayarak](https://github.com/frudotz/openwrt-cloudflare-tunnel/releases/download/Cloudflared/cloudflared.md) ulaşabilirsiniz. 

- ### 🪄 Cloudflared Kurulumu
> - OpenWRT kurulu modeminizin/routerınızın arayüzüne ulaşın.  
> - **`System > Software`** altından ilgili sekmeye ulaşın.  
> - **`Actions > Update Lists`** altından paket listesi güncellemenizi gerçekleştirin.  
> - Güncellemenin ardından **`Cloudflared`** aramasını yaparak ilgili paketi indirin. (8.4 MB)   
> - İndirme işlemi tamamlandıktan sonra işletim sisteminizin veya WinSCP'in komut penceresini açın.  
> - SSH bağlantısını kurup cihaza giriş yaptıktan sonra **`cloudflared`** yazarak servisi aktif edin.  
> - Akan yazılar bir süre durakladığında **`CTRL+C`** kombinasyonu ile işlemi durdurun.  

<p align="left">
  <img width="auto" height="154" src="https://media.discordapp.net/attachments/796061773795033169/1092380415614013532/1.png">
  <img width="auto" height="154" src="https://media.discordapp.net/attachments/796061773795033169/1092380415941148772/2-9.png">
  <img width="auto" height="232" src="https://media.discordapp.net/attachments/796061773795033169/1092382801929699369/10-14.png">
</p>

# 🚀 Cloudflare Tunnel Oluşturma
Cloudflare gösterge panelinden Zero Trust'a tıklayın, yönlendirildiğiniz sayfadan **`Access > Tunnels`** kısmına ilerleyin.  
Bu bölümde **`Create a tunnel`** butonuna tıklayın ve gelen sekmeden tünelinize isim vererek ilerlemeye devam edin.  

- #### 🌐 Konnektör Kurulumu (Install Connector)
> - Cloudflare'in sekmede sizinle paylaştığı kodu kopyalayın ve tünel erişim kodunuzu (Token) ayıklayın.  
> - WinSCP üzerinden cihazınıza resimlerde gösterildiği şekilde bağlanın ve **`/etc/init.d/`** yolunu izleyin.  
> - **`cloudflared`** dosyasını açıp içindeki kodları silin ve sizinle paylaştığımız kodları yapıştırın.  
> - Kodların içindeki **`YOUR_TUNNEL_TOKEN`** kısmına kendi tünel erişim kodunuzu (Token) yapıştırın.  
> - Dosyayı kaydedin ve SSH bağlantısı üzerinden **`service cloudflared restart`** komutunu girin.  
> - Bir dakikadan daha az bir süre içerisinde Cloudflare arayüzünde cihazınız belirecektir, belirdiğinde ilerleyin.  
  
- #### ⚙️ Tünel Yönlendirme (Route Tunnel)
> - Public hostname kısmından cihazınızı hangi adres ile yayınlayacağınızı belirleyebilirsiniz.  
> - Service kısmından ağınızdaki hangi cihazı internete çıkaracağınızı belirleyebilirsiniz.  
> - Tercihen **`main.frudotz.net`** adresi üzerinden ağımdaki ana modem cihazını yayınlayacağım.  

- #### 🔀 Diğer Cihazları İnternete Çıkarma
> - İlk ayarları tamamladığınızda yönlendirileceğiniz sayfadan üç noktaya tıklayıp **`Configure`** deyin.  
> - Üst kısımdan Public Hostname bölümüne ilerleyin ve **`Add a Public hostname`** butonuna tıklayın.  
> - Bu kısımda tercihen routerımı **`router.frudotz.net`** adresi üzerinden yayınlayacağım. 
> - *\*Yerel adresinizin sonuna port sayısı girerseniz birden fazla servisi yayınlayabilirsiniz.* 

<p align="left">
  <img width="auto" height="116" src="https://media.discordapp.net/attachments/796061773795033169/1092478832700833872/15-22.png">
  <img width="auto" height="115" src="https://media.discordapp.net/attachments/796061773795033169/1092478833170591834/23-27.png">
  <img width="auto" height="232" src="https://media.discordapp.net/attachments/796061773795033169/1092483393658302594/28-32.png">
</p>

# 😎 Hoş Geldin Cloudflare Argo Tunnel!
Bu aşamaya kadar bir hata yapmadıysanız birkaç dakika içinde tünel tam çalışır duruma gelecektir.  
Sizlere gösterebilmek üzere VPN açarak ilgili domain üzerinden cihazıma erişeceğim;  

<p align="left">
  <img width="410" height="auto" src="https://media.discordapp.net/attachments/796061773795033169/1092485824542675084/33.png">
  <img width="410" height="auto" src="https://media.discordapp.net/attachments/796061773795033169/1092485824794341466/34.png">
</p> 

# 💖 Özel Teşekkürler
Konfigürasyon düzenlemesi ve bilgi birikimiyle sağladığı destek için sevgili [@isnotallow](https://github.com/isnotallow)'a teşekkürler.
  
-----------
