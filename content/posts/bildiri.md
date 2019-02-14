---
title: "Gayrimerkezi bir dünyanın arifesinde iki yeni adım: GNU MediaGoblin ve GNU Taler"
date: 2019-02-14T14:46:32+03:00
draft: false
---

_Bu bildiri, Akademik Bilişim 2019 için verilmiştir._
_[Buraya tıklayarak](/59.pdf) bildiriyi PDF formatında indirebilirsiniz._

**Özet:** Kişisel verilerin güvenliği, internet özgürlüğü, ifade özgürlüğü ve bunların hepsini kapsayan özgür toplum kavramı gündeme geldiğinde, temel özgürlüklerin ve kişisel mahremiyetin teminini sağlayan yegane araçlar gayrimerkezi yapılardır. Dijital olarak, içinde bulunduğumuz gayrimerkezileşme sürecinde, özellikle son 10 yılda birçok önemli adım atılmıştır. Özgür yazılımlar sayesinde bugün, standart bir son kullanıcı bile rahatlıkla kendi servislerini kolaylıkla ayağa kaldırabilmekte ve yürütebilmektedir. Bu makalede, gayrimerkezi yapıların bir nebze geri kaldığı medya yayın platformları ve ödeme altyapısı noktaları için özgür yazılım topluluğuna _de facto_ yön veren GNU projesine dahil olan MediaGoblin ve Taler yazılımlarının hedefleri, bugünü ve yarını ele alınacaktır.

**Anahtar Sözcükler:** Ademimerkeziyet, Özgürlük, Özbarındırma, Özgür yazılım, İnternet

### 0. Giriş

“Decentralization”, Türkçe’siyle gayrimerkeziyet veya ademimerkeziyet; siyasi olarak _yerinden yönetim,_ anlamsal olarak _merkezin yokluğu_ anlamına gelmektedir \[1\]\[2\]. Siyaseten, yerel yönetimlerin merkezi yönetimlerden birtakım hak ve yetkileri devralması gibi bir anlam teşkil eder \[3\]. 

Özgür yazılımların çok önemli bir getirisi ve gereksinimi olan kişisel mahremiyet vukuu, bilgisayar ağları üzerinde faaliyet gösteren yazılımlar için gayrimerkezi yapıları da beraberinde getirmiştir. Günümüzde, özellikle de KVKK ve GDPR gibi düzenlemelerin de etkileriyle kişisel verilerin güvenliğini teşkil etmenin en olası yolu gayrimerkezi yapılardan geçmektedir. Çünkü gayrimerkezi sistemlerde; kullanıcıların kişisel verileri, kullanıcı tarafında saklanmakta ve kullanıcı tarafından verilen izinler doğrultusunda sistemin diğer kullanıcıları ile paylaşılmakta veya saklanmaktadır.

Çalışma; Solid, GNU Social, Mastodon, e\-posta sistemleri gibi artık internet çevresi ve özgür yazılım topluluklarında bilinirlik kazanmış sosyal ağ ve iletişim sistemlerinin haricinde, henüz yeteri kadar farkındalığın oluşmadığı medya paylaşımı ve ödeme sistemleri alanlarında birer çözüm olarak ortaya çıkan, GNU projesinin iki yeni paydaşı olan GNU MediaGoblin ve GNU Taler yazılımlarını, alternatif olarak sunuldukları sistemler ile kıyaslayıp, sunduğu avantajları ve eksiklikleri göz önüne sermek amacıyla hazırlanmıştır.

Çalışmanın ilk bölümünde kavramlar ve mevcut durum ele alınmakta, akabinde ise yazılımlar kendileri özelinde incelenmektedir. Son olarak ise gelinen nokta değerlendirilmiş ve öneriler sunulmuştur.

### 1. Merkezi ve gayrimerkezi yapılar

Günümüzde internet üzerinde yaygın biçimde kullanılan birçok servis, merkezi yapılara örnek teşkil etmektedir. 2019’un ilk haftası itibarıyla, dünya üzerinde yaklaşık 4 milyar 113 milyon internet kullanıcısı mevcuttur \[4\]. Bu veriden hareketle örneğin, merkezi bir sosyal ağ platformu olarak faaliyet gösteren Facebook, 2 milyar 395 milyon kullanıcı sayısıyla neredeyse internet erişimi olan her 100 kişiden 60’ı tarafından kullanılmaktadır \[5\]. Normal şartlarda gayrimerkezi olarak kullanılabilen e\-posta hizmeti dahi, 2018’in Ekim ayında 1.5 milyon kullanıcıya sahip olan Google Gmail ve 2016’nın Eylül ayında 780 milyon kullanıcıya sahip olan Apple iCloud servisleri marifetiyle _de facto _olarak merkezi hale gelmiştir \[6\] \[7\]. Son kullanıcılar haricinde, şirketler ve üniversiteler de bu tarz merkezi yapıları servis sağlayıcısı olarak yaygın biçimde kullanmaya başlamıştır. Bir araştırma şirketinin verilerine göre, 1 milyon 700 binden fazla alan adı, Google’ın **ücretli **özel mülk servis sağlayıcısı olan G Suite servisini kullanmaktadır \[8\]. Bunların yanı sıra, Türkiye’de mevcutta var olan 183 üniversitenin 91 tanesi bu tarz servis sağlayıcıları üzerinden e\-posta hizmeti sunmaktadır \[9\]. Üniversitelerin çok önemli bir çoğunluğunun kendi sunucularına ve bilgi işlem personeline sahip olduğu düşünüldüğünde, merkezi yapılara olan eğilim daha açıkça görülebilmektedir.

Gayrimerkezi yapılar ise, özellikle özgür yazılım kullanan bilgisayar ve internet kullanıcıları arasında hızla yayılmaktadır. Bunun sebepleri ise; kişisel mahremiyet hassasiyeti, sansür konuları, birçok merkezi servisin özel mülk JavaScript yazılımı kullanmayı zorunlu kılması, kullanıcıların genellikle teknik düzeyinin yüksek olması ve buna binaen kendi servis sunucularını daha kolay ayağa kaldırabilmeleri ve yönetebilmeleri şeklinde sıralanabilir. Ancak yine de, belirli alanlarda ortaya çıkan özgür yazılımların, özel mülk benzerleri gibi merkezi yapıda tasarlandıkları da gözden kaçmamalıdır. Örneğin bir anlık mesajlaşma yazılımı olan Telegram, hem istemci tarafında hem de sunucu tarafında özgür olmasına karşın, federasyon desteklemeyen ve merkezi bir yapıda tasarlanmıştır \[10, dipnot 1\]. Bunun da muhtemel sebebinin, kullanım kolaylığı, farklı sunucularda çalışan yazılımların uyumsuz olma ihtimali gibi durumlar olduğu düşünülmektedir.

Gayrimerkezi yapılar, federatif veya gayrifederatif olabilmektedir. Burada federasyon tanımı, farklı sunucularda çalışan yazılımların birbirilerini anlayabilmesi ve gerektiğinde aralarında konuşabilmesi anlamına gelmektedir. Örneğin; XMPP protokolü ve yazılımı gayrimerkezi ve federatif olarak tasarlanmıştır. Yazılımın doğası gereği, farklı XMPP sunucularında yer alan farklı kullanıcılar birbirileriyle rahatlıkla iletişim kurabilmektedir. Buna karşın, Open Whisper Systems’ın geliştirdiği Signal yazılımı gayrimerkezi olabilmekle birlikte, federatif olarak tasarlanmamıştır. Aynı sunucuda yer alan kullanıcılar servisi kullanabilmekte, ancak farklı sunucular birbiriyle konuşamamaktadır. Sonraki süreçte, Signal’e federasyon desteği kazandırmakla ilgili çalışmalar yapılmış olmakla birlikte, resmi Signal sunucuları henüz bu desteğe kavuşamamıştır.

Web servislerine federasyon desteği kazandırabilmek için, yine bir gayrimerkezi sosyal ağ sistemi olan pump.io tarafından geliştirilen ActivityPub protokolü, W3C tarafından standartlaştırılmıştır \[40\]. ActivityPub protokolü, sunucu\-istemci iletişiminde içerik yükleme, düzenleme, değiştirme ve silme; sunucu\-sunucu iletişiminde içerik aktarımı ve bildirim gönderimi işlevlerini yerine getirebilecek genel amaçlı API’leri sağlamaktadır. Mastodon, NextCloud, PeerTube gibi önemli gayrimerkezi federatif web servisleri ActivityPub protokolünü yazılımlarına entegre etmiştir \[41\].

### 1.1. Medya yayın platformları ve sorunları

Sosyal ağlar ve iletişim yöntemlerinin haricinde, yaygın kullanılan bir başka servis ise medya yayın platformlarıdır. Bu noktada medya kavramı; video, ses, müzik, belge, tasarım gibi her nevi içeriği kastetmek için kullanılmıştır. Yaygın olarak kullanılan medya paylaşım platformları için; YouTube, Vimeo, SoundCloud, Imgur, SlideShare gibi örnekler verilebilir. 

Video yayını konusunda YouTube tartışmasız lider konumundadır. Google’ın bir servisi olan, toplamda 5 milyardan fazla video yayınlanmış olan platforma, dakikada 300 saatten fazla video yüklenmektedir \[11\]. Bunun haricinde, yaklaşık her 3 internet kullanıcısından biri YouTube’u kullanmaktadır \[11\]. Platformda, standart videoların haricinde canlı yayınlar, ücretli abonelikler ve izleme listeleri gibi özellikler de bulunmaktadır. YouTube, gelirinin çok önemli bir bölümünü videoların arasında yayınladığı reklamlardan elde etmekte, bu gelirin de bir kısmını isteğe ve aktiviteye bağlı olarak video sahipleriyle paylaşmaktadır. Ayrıca YouTube üzerinde yapım şirketleri gibi firmaların kullanımı için oluşturulmuş kurumsal hesaplar da mevcuttur. Platformun herhangi bir yükleme ve izleme sınırı yoktur. Ancak YouTube, video harici herhangi bir yüklemeye izin vermemektedir.

Ses ve müzik paylaşımı için, merkezi bir seçenek olarak SoundCloud servisi ön plana çıkmaktadır. SoundCloud, kullanıcıların kendilerine ait olan sesleri ve müzikleri yüklemesi için kullanılan bir servistir. Aylık 76 milyon kullanıcıya ulaşan servise, yaklaşık 10 milyon kullanıcı yükleme yapmaktadır \[12\]. Toplamda 170 milyon adet ses yüklenen servise, dakikada 12 saatten fazla ses yüklenmektedir. Servis, kullanıcılara iki ana tip üyelik sunmaktadır. Ücretsiz üyelik, kullanıcılara 180 dakikalık yükleme sınırı koymaktadır. Ücretli üyelikte ise böyle bir sınır yoktur. Her iki tip üyelikte de, herhangi bir dinleme sınırı bulunmamaktadır \[13\]. SoundCloud, Creative Commons lisanslarını da desteklemektedir. Spotify veya Deezer gibi servisler, yalnızca yapımcılara açık olması ve kullanıcılara DRM’i zorlaması gibi sebepler nedeniyle bu çalışmanın konusuna dahil değildir. 

Fotoğraf ve resim paylaşımı için, birçok servis bulunmakla birlikte, en yaygın kullanılan servislerden biri Imgur’dur. Imgur, aslen Reddit için tasarlanmakla birlikte, her türden kullanıcıya açıktır \[14\]. Imgur’da genel bir yükleme sınırı olmamakla birlikte, IP adresi başına saatlik 50 gönderi sınırı bulunmaktadır. Ücretli üyelik ile bu sınır kaldırılabilmektedir. 2012 yılında 300 milyon fotoğraf yüklenen sistemde, toplam 364 milyar görüntülenme ve 42 petabayt veri transferine ulaşılmıştır \[15\]. Imgur’un verileri Amazon’un AWS sisteminde tutulmaktadır. Imgur’un galeri oluşturma, yorum, basit görsel düzenleme gibi özellikleri bulunmaktadır.

Üç boyutlu tasarım paylaşımı için, Thingiverse yaygın kullanılan servislerden biridir. Thingiverse üzerinde kullanıcılar, üç boyutlu yazıcı veya lazer kesim makineleriyle çıktı almaya uygun formatlarda tasarımlarını paylaşabilmektedir. Thingiverse, özel mülk üç boyutlu yazıcı üreten MakerBot firmasının bir servisidir \[16\]. Tasarımları tarayıcı üzerinde üç boyutlu olarak görüntüleyebilme, uygun olan tasarımları kısıtlı ölçüde düzenleyebilme, istenen tasarımları çatallayabilme gibi özellikleri olan Thingiverse’te yer alan bütün tasarımlar Creative Commons lisansları, GNU GPL veya BSD lisansları ile lisanslanmak zorundadır \[16\]. “No\-Commercial” şerhi bulunan Creative Commons lisansları haricinde geri kalan lisansların tamamının özgür lisanslar olması dikkat çekicidir. 

Çalışmada, belge paylaşımı için yaygın kullanımda olan bir servise rastlanmamıştır. 

Bu tip servislerde, kullanıcılar açısından birçok problem mevcuttur. Bu problemlerden ilki ve en önemlilerinden biri, platforma yüklenen verilerin geleceğinin meçhul olmasıdır. Örneğin, özellikle 2000’li yıllarda popüler bir görsel paylaşım platformu olan ImageShack, 2010’ların başında ücretsiz kullanıcıların fotoğraflarını silmeye başlamış, 2016 yılında ise bu fotoğrafları tamamen silmiştir \[17\]. Bu yüzden, 2000’lerde web üzerinde yapılan paylaşımlarda yer alan birçok fotoğraf yok olmuştur. 

E\-posta servisi de veren bir internet servis sağlayıcısı olan “E\-kolay.net”, ömür boyu internet ve e\-posta aboneliği taahhütü ile abonelik satmış \[18\], ancak e\-posta hizmetini 11 Nisan 2013 tarihinde sonlandırmıştır. 

Bir başka problem ise, kullanıcı verilerinin güvenliğidir. Gayrimerkezi yapılarda, kullanıcıların verileri kullanıcının kendi sunucusunda tutulur. Ancak merkezi yapılarda, bütün kullanıcıların verileri, ilgili servisin kendi sunucularında tutulmaktadır. Bu verilerin nasıl saklandığı, bu verilere kimlerin erişebildiği ise açıkça belirtilmemiştir. Ayrıca servisi sağlayan şirket, verilerin güvenliği yönünde taahhüt verse bile, sisteme erişim yetkisi olan bir çalışanın bütün verileri okuyabilme ihtimali yine de vardır. Bunların haricinde; birçok servis sağlayıcı, kullanıcıların verilerini üçüncü şahıslarla paylaşmakta veya başka şahıslara ücret karşılığında satmaktadır. Sunuculara yapılan herhangi bir saldırı durumunda da yine bu verilerin güvenliği tehlikeye girmektedir. 

Medya paylaşım platformları özelinde, sansür ve lisanslama sorunları da ortaya çıkmaktadır. Devletler, istediğinde ilgili servise veya içeriğe erişimi engelleyebilmektedir. Yukarıda adı geçen servislerden; Thingiverse hariç hepsi zaman zaman Türkiye’de erişime engellenmiş olmakla birlikte \[19\]\[20\], Imgur servisi halen daha Türkiye’den erişime engellenmiş durumdadır \[21\].

Lisanslama konusunda, YouTube üzerinde sınırlı seçenek sunulmaktadır. YouTube yalnızca iki lisans tipine izin vermektedir; bunlardan biri Standart YouTube Lisansı adında bir özel mülk lisans, diğeri ise Creative Commons Atıf lisansıdır \[22\]. Bunların haricindeki lisans tiplerine izin verilmemektedir. Dolayısıyla, örneğin GNU GPL v3\+ lisansı ile lisanslanmış bir videonun YouTube’a konulması teknik olarak mümkün değildir. Yalnızca GPL değil, Copyleft özelliğine sahip herhangi bir lisans için de bu durum problem teşkil etmektedir. SoundCloud üzerinde ise, varsayılan lisans yine bütünen özel mülkiyet lisansı olmakla birlikte, Creative Commons lisanslarının kullanımına müsaade edilmektedir \[23\].

Ayrıca, YouTube platformunda, kullanıcıların videolarına ekledikleri müzikler eğer YouTube’un anlaşmalı olduğu bir yapım şirketinin telif hakkına tabii ise, videonun açıklamalar kısmında bir uyarı çıkmakta ve ilgili videonun gelirlerinin bir kısmı \(videodan gelir elde edilse de edilmese de\) ilgili yapım şirketine aktarılmaktadır \[24\]. Aksi ihtimalde video silinebilmektedir. Sanatçıların kendi YouTube kanallarına yükledikleri kendi şarkılarında bile bu prosedür uygulanmaktadır. 

YouTube, ülke bazında sansür uygulamasına da sahiptir. Örneğin, Türkiye’de yayınlanmakta olan bir dizi YouTube’a yüklendiğinde, Türkiye’de o dizinin telif hakkına sahip olan yapımcı, videonun yalnızca Türkiye’de erişime engellenmesini isteyebilmektedir. Bu durumun birçok örneği vardır, örneğin YouTube’da popüler olan videoların %60’ı Almanya’da izlenememektedir \[11\]. 

Yasal durumlar ve telif hakkı konuları haricinde, keyfi sansür uygulamaları da yine YouTube üzerinde karşılaşılan sansür örneklerindendir. YouTube, istediği videoyu kullanım şartlarına uymadığı gerekçesiyle yayından kaldırabilmektedir. 2007 yılında Mısır protestolarından çektiği görüntüleri yayınlayan Wael Abbas isminde bir Mısırlı aktivistin YouTube hesabı, hiçbir gerekçe olmaksızın yayından kaldırılmıştır \[25\]. LGBT konularıyla ilgili videoların “Kısıtlanmış içerik” kapsamına alındığı, 18 yaşın altındaki kullanıcılar tarafından görüntülenmesinin engellendiği de birçok kullanıcı tarafından bildirilmiştir \[26\]. Birçok YouTube kanalının ise, “reklam yayınlamaya uygun olmayan içerik” yayınladığı iddiasıyla reklam gelirleri kesilmiştir \[26\]. Ayrıca, 2018 yılının başında Yeşil Nasim isminde bir YouTube kullanıcısı, “fırsat eşitsizliği” ve kanalındaki videoların haksız yere filtrelendiği iddialarıyla YouTube’un genel merkezine silahlı saldırıda bulunmuş, 4 YouTube çalışanını yaralamış, ardından intihar etmiştir. Bu olayın ardından YouTube, hiçbir sebep göstermeksizin Yeşil Nasim’in YouTube hesabını ve videolarını ortadan kaldırmıştır \[27\].

### 1.2. Ödeme altyapıları

Gayrimerkezi yapıların henüz tam olarak gelişemediği bir alan da ödeme altyapılarıdır. Günlük hayatta sıkça kullanılan nakit, kredi/banka kartı, yemek kartı, çek, senet, havale, EFT gibi yöntemlere göre, internet üzerinde ödeme yapma biçimleri daha kısıtlıdır. Birçok e\-ticaret sitesi yalnızca kredi/banka kartıyla ödeme almakta, bazı kuruluşlar ise havale/EFT seçeneğini de dahil etmektedir. Kredi/banka kartı ile ödemeler bankaların kendi sanal POS sistemleri veya İyzico, PayU gibi sanal POS aracı kuruluşları vasıtasıyla alınmaktadır. Havale/EFT ile ödemelerin ise, bankaların API’lerinin yetersiz oluşu nedeniyle çoğunlukla manuel kontrol edilerek onaylandığı yapılan araştırmanın sonucunda öğrenilmiştir. Bir banka hesabına veya kredi kartına sahip olmayanlar ve 18 yaşın altındaki kullanıcılar için birkaç farklı kuruluş tarafından piyasaya sürülen “ödeme kartları” da mevcuttur \[28\]\[29\]\[30\]. Bu tip ödeme kartlarında; elden, ATM’lerden veya havale ile karta nakit para yüklenebilmekte, daha sonra bu para e\-ticarette veya standart POS’larda kullanılabilmektedir. Bu sayede çevrimiçi ödemelerde nakit kullanılamaması sorunu aşılmaya çalışılmıştır. Yine de bütün kartlar öncelikle bankalara, onların vasıtasıyla MasterCard, Visa gibi uluslararası birkaç kuruluşa veya Türkiye’de tek olan BKM’nin Troy sistemine bağlıdır \[31\]. Bu kuruluşlar zaman zaman ödemelere sansür uygulayabilmektedir. Daha önce MasterCard ve Visa, WikiLeaks’e yayınladığı belgelerden dolayı hizmet vermeyi bırakmıştır \[34\].

Bunların haricinde, uluslararası olarak faaliyet gösteren PayPal, Payoneer, WebMoney gibi kuruluşlar da mevcuttur. Bunlar banka değil, ödeme aracısı olarak hizmet vermektedir. Bu tip aracılar sayesinde, kullanıcılar kendi web siteleri üzerinden hiçbir yere başvuru yapmaksızın açtıkları basit bir kullanıcı hesabı sayesinde ödeme alabilmektedirler. Ancak bu tarz kuruluşların da oluşturduğu sıkıntılar vardır. Örneğin, PayPal daha önce hiçbir yasal sebep olmaksızın gazeteciler, içerik yayıncıları, yazılım geliştiricileri gibi farklı alanlardan birçok kullanıcının hesaplarını bloke etmiştir \[32\]\[33\]. Ayrıca PayPal, WikiLeaks’in de hesaplarına bloke koymuştur \[35\]. Bunların haricinde, devletler de bu tarz ödeme altyapılarının kullanımını engelleyebilmektedir. Örneğin PayPal’ın Türkiye’de kullanılması BDDK tarafından engellenmiştir \[36\]. Doğrudan servis kaynaklı sorunlar da mevcuttur, örneğin WebMoney ile alınan ödemeler Türkiye’deki banka hesaplarına doğrudan aktarılamamaktadır. 

Bu yöntemlerin haricinde bir diğer yöntem ise kriptodövizlerdir. Kriptodövizler, gayrimerkezi olarak tasarlanmış değişim araçlarıdır. Kriptodövizlere dördüncü bölümde ayrıntılı olarak değinilecektir.

### 3. GNU MediaGoblin

Medya paylaşım platformları özelinde yer alan eksikliği tamamlamak için GNU Projesi kapsamında 2011 yılında MediaGoblin isminde bir yazılım geliştirilmeye başlanmıştır \[37\]. MediaGoblin; birçok dijital medya biçimini destekleyen, gayrimerkezi, federatif, özelleştirilebilir, özbarındırmalı bir medya yayın platformudur \[38\]. MediaGoblin’in dikkat çeken özellikleri arasında; ActivityPub üzerinden federasyon desteği, bütünen özelleştirilebilir olması, eklenti desteği, pek çok medya biçimini desteklemesi ve hatta medya desteği eklenebilmesi, gelişmiş izin yönetimi, bildirim destekli yorum sistemi sayılabilir \[39\]. MediaGoblin’in yayınlanan son sürümü 0.9 numaralı sürümü olup halen daha aktif geliştirme aşamasındadır.

### 3.1. GNU MediaGoblin’in mevcut yapılarla karşılaştırılması

MediaGoblin’i yaygın kullanılan merkezi yapılardan ayıran en önemli nokta, özgür yazılım olmasıdır. YouTube veya SoundCloud gibi servisler sunucu tarafında özel mülk olduğu gibi, kullanıcılarına da özel mülk JavaScript kodu servis etmektedir. Ayrıca bu tarz servislerin çoğunlukla herkese açık API’leri olmamakta, dolayısıyla alternatif bir istemci yapmak imkansız hale gelmektedir. 

MediaGoblin özgür yazılım olduğu için, her noktası istenilen veya ihtiyaca uygun olacak şekilde düzenlenebilmekte ve yeniden dağıtılabilmektedir \[42\]. Örneğin; bir yayıncı MediaGoblin’i e\-kitaplarını DRM’siz olarak ücret karşılığında yayınlayacak şekilde yapılandırabilmektedir. Aynı şekilde bir sivil toplum kuruluşu, oluşturduğu medyaları kendi bağış sistemine entegre edebilmektedir. ActivityPub desteği ile birlikte, şu an için sınırlı olsa da federasyon desteğine sahip olan MediaGoblin; teorik olarak NextCloud gayrimerkezi dosya depolama servisleri, PeerTube gayrimerkezi video paylaşım platformları, gayrimerkezi mikroblog servisleri ile rahatlıkla entegre edilebilir ve kullanılabilir. MediaGoblin’e farklı kimlik doğrulama sistemleri de eklenebilmektedir. Bu sayede MediaGoblin, yine teorik olarak NextCloud gibi farklı bir gayrimerkezi servis ile birlikte, ayrıca bir kimlik doğrulamasına ihtiyaç duymaksızın eklenti gibi çalışabilmektedir.

Bir önceki bölümde aktarılan merkezi servislerin hepsi, yalnızca tek bir medya biçimi barındırmak için tasarlanmıştır. Dolayısıyla; hem müziklerini, hem videolarını hem de fotoğraflarını paylaşmak isteyen bir kullanıcı, üç farklı servise üye olmak zorunda, bir başka yönden üç farklı şirketin müşterisi olmak zorundadır. MediaGoblin, özellikle bu yönden bakıldığında son derece gelişmiş bir sistem olarak tasarlanmıştır. Birçok farklı video ve ses biçimini destekleyen MediaGoblin’e bir video veya ses yüklendiğinde, ilgili medya HTML5 tarafından desteklenen özgür WebM ve Vorbis biçimlerine dönüştürülmekte, bu sayede neredeyse her türlü sistemle uyumlu ve özgür bir yayın sağlanmaktadır \[43\]. Standart JPEG ve PNG resim biçimlerinin yanı sıra, ASCII sanat desteği de sunulmaktadır. MediaGoblin, PDF biçiminde belgeler ve sunular için de destek sunmaktadır. Yapılan araştırmada bu tarz belgelerin yayınlanması için kurulmuş ve yaygın kullanılan bir platforma rastlanmamıştır. Bunların haricinde, üç boyutlu modeller için de önizleme ve render desteği sunulmaktadır. Bu desteğin sağlanmasında, özgür donanım tasarımı ile üç boyutlu yazıcılar geliştiren bir firma olan LulzBot’tan, Thingiview kütüphanesinden ve özgür bir yazılım olan Blender’dan yararlanılmıştır \[44\]. Sonuç olarak MediaGoblin, birçok merkezi servis için tek başına, gayrimerkezi ve federatif olarak özelleştirilebilir ve ölçeklenebilir bir alternatif sunmaktadır.

### 4. GNU Taler

GNU Taler, 2014 yılında geliştirilmeye başlanan bir elektronik ödeme sistemidir \[45\]. Kriptodövizlerin ödeme yöntemi olarak kullanılmasında karşılaşılan yüksek komisyonlar, chargeback olmaması, madencilik yüzünden kaynakların tüketilmesi ve oluşan karbon salınımı, kapalı anahtar kaybedildiğinde varlıkların da kaybedilmesi, yasal yönden ispat zorluğu gibi sorunlar ile, kredi kartı ödemelerinde karşılaşılan anonimliğin olamaması, yüksek komisyonlar, altyapı bağımlılığı, phishing, kartın çalınması durumunda yaşanan kayıplar gibi sorunlara çözüm olarak ortaya çıkmıştır. GNU Taler’ın asıl amacı, günlük hayatta nakit paranın kullanım kolaylığını ve avantajlarını dijital ortama taşıyabilmektir. 

### 4.1. GNU Taler, kriptodöviz ve geleneksel ödeme yöntemleri

GNU Taler, kriptodövizler ile tamamen farklı bir sistem ile çalışmaktadır. Taler üzerinde herhangi bir blok zincir veya benzeri yapı bulunmamaktadır. Blok zincir temelli kriptodövizler gibi bütünen dağıtık yapıda değil, birbirine bağlı merkezler şeklinde faaliyet göstermektedir. 

Aşağıdaki şemada sistemin işleyişi görülmektedir:

# TODO: fotoğraf

Kullanıcı öncelikle aracı takas sistemine istediği bir miktarda para yatırmakta, daha sonra yatırdığı para cüzdanına geçmektedir. Görselde bankalar üzerinden bir gösterim olsa da, rahatlıkla bir gazete bayiinden veya internet kafeden elden yükleme yapılmasında teorik bir engel yoktur. Yüklenen para, kullanıcının cüzdanına kredi olarak yüklenmektedir. Daha sonra bu kredi, kullanıcının tarayıcısına kurduğu bir Taler cüzdan eklentisi marifetiyle, Taler destekleyen satıcılarda harcanabilmektedir. Satıcı, isterse aracı üzerinden parayı doğrudan banka hesabına alabilmekte, isterse yine bu krediyi farklı yerlerde kullanabilmektedir. 

Taler, farklı para birimlerini de desteklemektedir. Bir kullanıcı, cüzdanında USD, TRY, Bitcoin gibi para birimleri saklayabilmekle birlikte, sanal para birimleri oluşturulmasında da teorik bir engel bulunmamaktadır. Ancak, sistem şimdilik para birimleri arasında kur dönüşümü yapılmasını desteklememektedir \[46\]. 

Taler’ın sunduğu en önemli özellikler; özgürlük, güvenlik, mahremiyet, uyumluluk, esneklik ve stabilitedir. Taler bütünen özgür yazılım olduğu için, özel mülk sanal POS API’lerine bağımlılık sorunlarını çözmekte, ayrıca kullanıcıları özel mülk JavaScript çalıştırma zorunluluğundan kurtarmaktadır. Taler’in cüzdanları varsayılan olarak dijital ortamda bulunmakta, ancak cüzdanları kaybetmemek için fiziksel yedekleri alınabilmektedir. Taler üzerinde yapılan bir ödemede, tarafların birbirilerini tanımasına gerek yoktur, bu yönden nakit ödemeye çok benzemektedir. Kredi kartı numarası girmek, OTP doğrulaması yapmak gibi bir işleme gerek olmadığı için çok daha hızlı ve güvenli bir şekilde ödemeler gerçekleştirilebilir. Taler bir kriptodöviz olmadığı için, cüzdana yüklenen varlığın değeri kriptodövizler gibi sürekli olarak değişmemektedir, bu sayede hem satıcılar hem de alıcılar için oldukça stabil bir yapıdır. Ayrıca özgür yazılım olması ve oluşturulan SDK sayesinde, istenilen yazılıma veya yapıya kolayca entegre edilebilmektedir \[47\]. 

GNU Taler’ın 2018 yılında operasyonel hale gelmesi hedeflenmişse de, bu hedef tutturulamamıştır \[45\].

### 5. Sonuç, gelinen nokta ve öneriler

Mevcutta gelinen noktaya bakıldığında, her iki yazılımın da henüz emekleme aşamasında olduğu görülmektedir. Bu tarz sistemler, ilk bölümde belirtilen yazılımların çeşitli sorunlarını aşma yönünde şimdiden çok büyük bir umut vaat etmektedir. Özellikle merkezi yapıların getirdiği gözetim ve sansür sorunlarını çözmenin yegane yolu, özgür yazılımlar ve gayrimerkezi/federatif yapılardan geçmektedir. Özellikle 2016 yılı ve sonrasında çok önemli adımlar atılan özgür yazılım ve gayrimerkeziyet konularında, halen daha atılması gereken çok adım, yapılması gereken çok iş vardır. Özellikle MediaGoblin’in federasyon desteğinin tamamlanması Özgür Yazılım Vakfı tarafından da “Yüksek Öncelikli Proje” olarak sınıflandırılmıştır. GNU Taler özelinde de aracılar arasındaki federasyon sisteminin düzenlenmesi, mobil ödeme desteğinin sağlanması gibi adımlar ehemmiyet arz etmektedir. Ayrıca Taler’ın ülkeler çapında bankacılık sistemleri ve firmalar arasında yaygınlık kazanması, kullanılabilir kılınması ve entegre edilmesi bugün çok uzun bir yolculuk olarak karşımıza çıkmaktadır. Sistemleri var eden paydaşlarıdır, dolayısıyla bu adımları atabilmek için; kullanıcıların bilinçlendirilmesi, şirketlerin ve kurumların özgür yazılımlara geçmek yönünde atılımlar sağlaması, devletlerin de bunun gibi yeniliklere açık olması elzemdir. 

### 6. Kaynakça

\[1\] TDK Genel Türkçe Sözlük, “ademimerkeziyet” maddesi

\[2\] Nişanyan, Sevan, Nişanyan Sözlük – Sözcüklerin Soyağacı, 2018

\[3\] TDK Genel Türkçe Sözlük, “yerinden yönetim” maddesi

\[4\] Worldometers.info – Internet user live statistics [https://worldometers.info](https://worldometers.info)

\[5\] Internet Live Statistics – Facebook usage rate \([https://internetlivestatistics.com](https://internetlivestatistics.com/)\)

\[6\] Gmail official Twitter account \- [https://twitter.com/gmail/status/1055806807174725633?ref_src=twsrc%5Etfw](https://twitter.com/gmail/status/1055806807174725633?ref_src=twsrc%5Etfw)

\[7\] Eddy Cue and Craig Federighi, Apple Inc., John Cue’s podcast, [https://daringfireball.net/thetalkshow/2016/02/12/ep-146](https://daringfireball.net/thetalkshow/2016/02/12/ep-146)

\[8\] SimiliarTech G Suite usage report, 2018 December

\[9\] Yücel, Necdet, Üniversiteler e-posta bayrağını nasıl kaybetti?, 2017 [https://www.nyucel.com/2017/04/universiteler-eposta-bayragn-nasl.html](https://www.nyucel.com/2017/04/universiteler-eposta-bayragn-nasl.html)

\[10\] Telegram resmi sitesi, FAQ bölümü, [https://telegram.org/faq](https://telegram.org/faq), Can I run Telegram using my own server?

\[11\] OmniCore Agency, YouTube by Numbers: YouTube Analytics

\[12\] DMR Stats, SoundCloud Usage Statistics 2018.

\[13\] SoundCloud resmi sitesi, [https://soundcloud.com](https://soundcloud.com)

\[14\] Imgur’un sahibi Alan Schaaf tarafından yazılan Reddit gönderisi, [https://www.reddit.com/r/reddit.com/comments/7zlyd/my_gift_to_reddit_i_created_an_image_hosting/](https://www.reddit.com/r/reddit.com/comments/7zlyd/my_gift_to_reddit_i_created_an_image_hosting/)

\[15\] Imgur Best of 2012, [https://imgur.com/bestof2012](https://imgur.com/bestof2012)

\[16\] Thingiverse, [https://www.thingiverse.com/about/](https://www.thingiverse.com/about/)

\[17\] [https://www.archiveteam.org/index.php?title=ImageShack](https://www.archiveteam.org/index.php?title=ImageShack)

\[18\] Web üzerinde yer alan kullanıcı yorumlarından bu sonuca varılmıştır.

\[19\] [https://www.sozcu.com.tr/2014/teknoloji/soundcloud-coma-erisim-engellendi-446604/](https://www.sozcu.com.tr/2014/teknoloji/soundcloud-coma-erisim-engellendi-446604/)

\[20\] [http://tr.wikipedia.org/wiki/YouTube%27a_T%C3%BCrkiye%27den_eri%C5%9Fimin_engellenmesi](http://tr.wikipedia.org/wiki/YouTube%27a_T%C3%BCrkiye%27den_eri%C5%9Fimin_engellenmesi)

\[21\] Imgur için Ankara 14. İdare Mahkemesi tarafından karar verildi.

\[22\] [https://support.google.com/youtube/answer/2797468?hl=tr](https://support.google.com/youtube/answer/2797468?hl=tr)

\[23\] SoundCloud Terms of Use [https://soundcloud.com/terms-of-use](https://soundcloud.com/terms-of-use)

\[24\] [https://support.google.com/youtube/answer/7680188?hl=tr](https://support.google.com/youtube/answer/7680188?hl=tr)

\[25\] [http://edition.cnn.com/2007/WORLD/meast/11/29/youtube.activist/](http://edition.cnn.com/2007/WORLD/meast/11/29/youtube.activist/)

\[26\] [https://kotaku.com/why-youtubers-are-freaking-out-about-money-and-censorsh-1786032317](https://kotaku.com/why-youtubers-are-freaking-out-about-money-and-censorsh-1786032317)

\[27\] [https://www.bbc.com/turkce/haberler\-dunya\-43639524](https://www.bbc.com/turkce/haberler\-dunya\-43639524)

\[28\] [https://ininal.com](https://ininal.com)

\[29\] [https://papara.com](https://papara.com)

\[30\] [https://paycell.com.tr](https://paycell.com.tr)

\[31\] Anılarla ve Fotoğraflarla Türkiye’nin Kartlı Ödeme Sistemleri Tarihi, BKM Yayınları

\[32\] [https://www.independent.co.uk/news/world/americas/paypal\-bans\-alex\-jones\-infowars\-far\-right\-youtube\-twitter\-a8549851.html](https://www.independent.co.uk/news/world/americas/paypal\-bans\-alex\-jones\-infowars\-far\-right\-youtube\-twitter\-a8549851.html)

\[33\] [http://en.wikipedia.org/wiki/PayPal\#/Criticism](http://en.wikipedia.org/wiki/PayPal\#/Criticism)

\[34\] [http://www.hurriyet.com.tr/gundem/wikileaks-ten-mastercard-ve-visa-ya-agir-misilleme-16488653](http://www.hurriyet.com.tr/gundem/wikileaks-ten-mastercard-ve-visa-ya-agir-misilleme-16488653)

\[35\] [https://wikileaks.org/PayPal\-freezes\-WikiLeaks\-donations.html](https://wikileaks.org/PayPal\-freezes\-WikiLeaks\-donations.html)

\[36\] PayPal resmi açıklama \- [https://www.paypal.com/tr/webapps/mpp/home](https://www.paypal.com/tr/webapps/mpp/home)

\[37\] [https://directory.fsf.org/wiki/Mediagoblin](https://directory.fsf.org/wiki/Mediagoblin)

\[38\] [https://mediagoblin.org](https://mediagoblin.org/)

\[39\] [https://mediagoblin.org/pages/tour](https://mediagoblin.org/tour.html)

\[40\] [https://www.w3.org/TR/2018/REC-activitypub-20180123/](https://www.w3.org/TR/2018/REC-activitypub-20180123/)

\[41\] [https://activitypub.rocks/implementation\-report/](https://activitypub.rocks/implementation\-report/)

\[42\] [http://git.savannah.gnu.org/cgit/mediagoblin.git/plain/COPYING](http://git.savannah.gnu.org/cgit/mediagoblin.git/plain/COPYING)

\[43\] [https://mediagoblin.org/news/mediagoblin\-0.3.0\-rise\-of\-the\-robogoblins.html](https://mediagoblin.org/news/mediagoblin\-0.3.0\-rise\-of\-the\-robogoblins.html)

\[44\] [https://mediagoblin.org/news/3d-support.html](https://mediagoblin.org/news/3d-support.html)

\[45\] [https://taler.net](https://taler.net/)

\[46\] [https://taler.net/en/faq.html](https://taler.net/en/faq.html)

\[47\] [https://docs.taler.net/en/](https://docs.taler.net/en/)





\[Dipnot 1\] Telegram’ın resmi sunucu yazılımı özgür olmamasına rağmen, MTProto protokolü özgür olduğu için, sunucu tarafı gayriresmi olarak yazılmıştır \(bkz. telegramd\)


