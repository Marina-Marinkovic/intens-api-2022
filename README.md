mvn clean package
docker build -t intens-demo:1.0 .
docker run -d --name demo-app -p 8088:8088 intens-demo:1.0 
docker tag intens-demo:1.0 marinamarinkovic/intens-demo:1.0
docker push marinamarinkovic/intens-demo:1.0 
kubectl apply -f k8s/

Koristila sam NodePort jer je ovo demo projekat, ali mu je potrebno pristupiti, iz tog razloga je ovaj tip idealan za testiranje. U realnoj situaciji bi se koristion LoadBalancer.

Sto se GitHub workflow-a tice, koristila sam neke predefinisane akcije poput actions/checkout@v4, actions/setup-java@v4 i docker/login-action@v3, sto je ubrzalo i pojednostavilo pisanje koda. 

Zbog toga sto sam koristila Kubernetes, GitHub Actions ne bi mogao da primeni novu sliku na mom racunaru, te sam ostavila poruku u Job Summary sa uputstvom za rucnu primenu. 

Postavila 2 slike na DockerHub - jednu sa GitHub hash kodom, kao i jednu sa latest kodom, kako bi se na lokalnom racunaru mogle samo pokrenuti komande iz Job Summary-ja, bez menjanja deployment fajla, u kom je podesen Allways kao imagePullPolicy. 