# Exemples de code
## Signature
```ruby
def sign_request(request, secret_key)
  #encode base 64
  policy = Base64.strict_encode64(request)

  # Sign policy with secret key
  digest = OpenSSL::Digest.new('sha1')
  hmac=OpenSSL::HMAC.hexdigest(digest, secret_key, policy)

  # encode base 64
  signature = Base64.strict_encode64(hmac)
  signature
end
```

```csharp
private string SignRequest(string request, string secretKey)
{
    // encode base 64
    string policy = System.Convert.ToBase64String(System.Text.ASCIIEncoding.ASCII.GetBytes(request));
    // hmac-sha1 with secretKey
    var digest = new HMACSHA1(System.Text.ASCIIEncoding.ASCII.GetBytes(secretKey));
    digest.Initialize();
    var tmp = BitConverter.ToString(digest.ComputeHash(Encoding.ASCII.GetBytes(policy)));
    // remove "-" and downcase
    var hmac = tmp.Replace("-", "").ToLower();
    // encode base64
    string signature = System.Convert.ToBase64String(System.Text.ASCIIEncoding.ASCII.GetBytes(hmac));
    return signature;
}
```
Exemple de fonction permettant de calculer une signature.

###Function parameters
Nom | Description
------- | ---------
request | Chaine à crypter
secret_key | Clé de cryptage

###Function return
Nom | Description
------- | ---------
retour | Chaine cryptée


## Headers

```ruby
def make_hearders_request(request, withshop = false)
  jeton = rand(99999999).to_s
  request["FIDELISA_JETON"] = jeton
  request["FIDELISA_PROVIDER"] = @provider
  request["FIDELISA_PROVIDER_KEY"] = sign_request(@provider + jeton, @provider_key )

  if (withshop)
    request["FIDELISA_APIUSER"] = @shop
    request["FIDELISA_APIUSER_KEY"] = sign_request(@shop + jeton, @shop_key )
  end
end
```

```csharp
public void MakeHeadersRequest(HttpWebRequest request, bool withshop = false)
{
    Random rnd = new Random();
    int jeton = rnd.Next(99999999);
    request.Headers.Add("FIDELISA_JETON", jeton.ToString());
    request.Headers.Add("FIDELISA_PROVIDER", provider);
    request.Headers.Add("FIDELISA_PROVIDER_KEY", SignRequest(provider + jeton, providerKey));
    if (withshop)
    {
        request.Headers.Add("FIDELISA_APIUSER", shop);
        request.Headers.Add("FIDELISA_APIUSER_KEY", SignRequest(shop + jeton, shopKey));
    }
}
```

Fabrique des entêtes Fidelisa d'une requête

###Function parameters
Nom | Description
------- | ---------
request | Requête à signer
withshop | Requête de type shop ? true/false


## Get
```ruby
def get_programs
  http = Net::HTTP.new(@uri.host, @uri.port)
  http.use_ssl = true

  request = Net::HTTP::Get.new("/api/shops/programs")
  make_hearders_request(request, true)
  response = http.request(request)
  body = JSON.parse(response.body)
  body["programs"]
end
```

```csharp
public Programs GetPrograms()
{
    String requestUrl = HOST_FIDELISA + "/api/shops/programs";
    HttpWebRequest request = WebRequest.Create(requestUrl) as HttpWebRequest;
    MakeHeadersRequest(request, true);

    using (HttpWebResponse response = request.GetResponse() as HttpWebResponse)
    {
        DataContractJsonSerializer jsonSerializer = new DataContractJsonSerializer(typeof(Programs));
        Object objResponse = jsonSerializer.ReadObject(response.GetResponseStream());
        return objResponse as Programs;
    }
}
```

Exemple d'appel d'une fonction Get (Liste des programmes)

###Function parameters
Nom | Description
------- | ---------

###Function return
Nom | Description
------- | ---------
retour | Tableaux de programmes

## Post

```ruby
def init_shop
  http = Net::HTTP.new(@uri.host, @uri.port)
  http.use_ssl = true

  request = Net::HTTP::Post.new("/api/shops/init")
  request['Content-Type'] = 'application/json'
  make_hearders_request(request, false)
  request.body = ({ :shop => { "user_email" => @shop_mail } }).to_json
  response = http.request(request)
  body = JSON.parse(response.body)
end
```

```csharp
public Shop InitShop()
{
    String requestUrl = HOST_FIDELISA + "/api/shops/init";
    HttpWebRequest request = (HttpWebRequest)WebRequest.Create(requestUrl);
    request.Method = "POST";
    MakeHeadersRequest(request);
    request.ContentType = "application/json; charset=utf-8";

    Shop shop = new Shop { userMail = shopMail };
    DataContractJsonSerializer ser = new DataContractJsonSerializer(shop.GetType());
    MemoryStream ms = new MemoryStream();
    ser.WriteObject(ms, shop);
    String json = Encoding.UTF8.GetString(ms.ToArray());
    StreamWriter writer = new StreamWriter(request.GetRequestStream());
    writer.Write(json);
    writer.Close();

    using (HttpWebResponse response = request.GetResponse() as HttpWebResponse)
    {
        DataContractJsonSerializer jsonSerializer = new DataContractJsonSerializer(typeof(Shop));
        Object objResponse = jsonSerializer.ReadObject(response.GetResponseStream());
        return objResponse as Shop;
    }

}
```

Exemple d'appel d'une fonction Post (Initialisation du shop)

###Function parameters
Nom | Description
------- | ---------

###Function return
Nom | Description
------- | ---------
retour | Le shop initialisé
