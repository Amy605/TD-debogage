# Boutique Diayma


## 1. Projets de la solution
- Un seul projet : `Diayma.csproj` (dossier P2FixAnAppDotNetCode)

## 2. Version du SDK .NET
- Framework cible du projet : netcoreapp2.0 (.NET Core 2.0)
- SDK installé : 2.1.818 (fixé avec global.json), en plus du SDK 10.0.403
- 
### Bug 1 : Le stock ne diminue pas après une commande
- Où:page d'accueil, colonne « Stock »
- Reproduction :ajouter un produit au panier, passer la commande et la terminer, puis revenir à l'accueil
- Résultat obtenu : le stock reste inchangé (ex. 20)
- Résultat attendu : le stock diminue de la quantité commandée

### Bug 2 : prix incohérents
- Où :toutes les pages
- Constat :les prix affichés en euros (ex. Galaxy A25 à 130 000,00 €) sont incohérents comment un galaxy A25 peut couter 130 000 euros 
- Résultat attendu : prix cohérents avec la devise


## 3. Parcours d'exécution et débogage (Tâche 8)

| Ordre | Namespace | Classe | Méthode | Mode | Pourquoi |
| :---: | :--- | :--- | :--- | :---: | :--- |
| **1** | `P2FixAnAppDotNetCode` | `Program` | `Main(string[] args)` | **F10 / F5** | Point d'entrée principal de l'application .NET. Il configure et lance le serveur WebHost. |
| **2** | `P2FixAnAppDotNetCode` | `Startup` | `Startup(IConfiguration)` | **F10** | Constructeur de la classe de démarrage. Initialise la configuration de l'application. |
| **3** | `P2FixAnAppDotNetCode` | `Startup` | `ConfigureServices(IServiceCollection)` | **F10** | Enregistre les services dans le conteneur d'injection de dépendances (repositories, services, cart, etc.). |
| **4** | `P2FixAnAppDotNetCode` | `Startup` | `Configure(IApplicationBuilder, IHostingEnvironment)` | **F10** | Configure le pipeline d'exécution des requêtes HTTP (middleware, routage, MVC). |
| **5** | `P2FixAnAppDotNetCode.Controllers` | `ProductController` | `ProductController(...)` | **F10** | Constructeur du contrôleur d'accueil. Reçoit les services `IProductService` et `ILanguageService`. |
| **6** | `P2FixAnAppDotNetCode.Controllers` | `ProductController` | `Index()` | **F11** | Méthode d'action de la page d'accueil qui appelle `_productService.GetAllProducts()` à la ligne 21. |
| **7** | `P2FixAnAppDotNetCode.Models.Services` | `ProductService` | `GetAllProducts()` | **F11** | Couche service (ligne 29). Délègue la récupération des produits au repository `_productRepository.GetAllProducts()`. |
| **8** | `P2FixAnAppDotNetCode.Models.Repositories` | `ProductRepository` | `GetAllProducts()` | **F10** | Accès aux données (ligne 41). Récupère le stock, filtre les produits disponibles (`Stock > 0`), puis les trie par nom. |
| **9** | `P2FixAnAppDotNetCode.Models.Services` | `ProductService` | `GetAllProducts()` | **Maj + F11** | Remontée dans la couche service pour convertir le tableau de produits en liste (`ToList()`). |
| **10** | `P2FixAnAppDotNetCode.Components` | `CartSummaryViewComponent` | `CartSummaryViewComponent(...)` | **F10** | Instanciation du composant d'affichage du résumé du panier présent dans le header de la page. |
| **11** | `P2FixAnAppDotNetCode.Components` | `CartSummaryViewComponent` | `Invoke()` | **F5** | Rendu de la vue partielle `View(_cart)` pour afficher le nombre d'articles et le total du panier. |
| **12** | `P2FixAnAppDotNetCode.Controllers` | `CartController` | `CartController(...)` | **F10** | Déclenché lors d'une action utilisateur sur le panier (ex: clic sur "Ajouter au panier"). |
| **13** | `P2FixAnAppDotNetCode.Controllers` | `CartController` | `Index()` / `AddToCart(...)` | **F10** | Traite l'ajout de l'article ou l'affichage de la page de gestion du panier. |
| **14** | `P2FixAnAppDotNetCode.Controllers` | `OrderController` | `OrderController(...)` | **F10** | Déclenché lors du clic sur le bouton de commande ("Checkout"). Injecte `ICart` et `IOrderService`. |
| **15** | `P2FixAnAppDotNetCode.Controllers` | `OrderController` | `Index()` | **F5** | Affiche le formulaire de saisie des informations de commande. |


## 4. Lien de téléchargement de l'exécutable 
- [Télécharger l'exécutable Windows (.zip)](https://drive.google.com/drive/u/0/my-drive)
