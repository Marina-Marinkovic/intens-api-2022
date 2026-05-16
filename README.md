## Odluke u toku rada

Koristila sam NodePort servis jer je u pitanju demo projekat kojem je potrebno pristupiti lokalno. Za ovakav tip aplikacije NodePort je jednostavno i praktično rešenje za testiranje. U produkcionom okruženju bi se koristio LoadBalancer.

Što se GitHub Actions workflow-a tiče, koristila sam predefinisane akcije poput:
- actions/checkout@v4
- actions/setup-java@v4
- docker/login-action@v3

kako bih ubrzala i pojednostavila CI/CD pipeline.

Pošto je Kubernetes pokrenut lokalno, GitHub Actions nema direktan pristup klasteru, pa sam u Job Summary delu workflow-a ostavila uputstvo za ručnu primenu nove verzije aplikacije.

Na Docker Hub su postavljene dve verzije slike:
- verzionisana slika označena GitHub commit hash-om
- latest tag

Kubernetes deployment koristi latest tag uz imagePullPolicy: Always, kako bi lokalni klaster prilikom redeploy-a uvek povukao najnoviju verziju slike bez izmene deployment fajla.

### Link

Aplikaciji se može pristupiti putem:
http://localhost:30008/

Nakon primene promena koda, može se proveriti stanje komandom "kubectl get pods".