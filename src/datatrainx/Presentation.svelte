<script>

    import * as animateScroll from "svelte-scrollto";
    import {layoutStore} from "../stores";
    import Faceapi from "./utils/Faceapi.svelte";
    import Logo from "./layout/Logo.svelte";

</script>
<style>
    .tile.is-ancestor {
        margin-top: 0;
    }
    .notification {
        padding: 1.25rem 1.5rem;
    }
    h2{
        text-align: center;
        font-size: 1.5em;
        font-weight: bold;
        margin-bottom: 8px;
    }
    .link{
        text-decoration: underline;
        cursor: pointer;
    }
    .link:hover{
        font-weight: bold;
    }
    p{
        text-align: justify;
        margin-bottom: 1em;
    }
</style>
  <div class="container">
      <div class="tile is-ancestor">
          <div class="tile is-vertical is-8">
              <div class="tile">
                  <div class="tile is-parent is-vertical">
                      <article class="tile is-child notification is-primary">
                          <h2>Obtenir son profil d'apprenant</h2>
                          <div class="buttons are-medium">
                              <button class="button are-medium center is-link is-rounded"  on:click ={() => layoutStore.setLayout("start")}>
                                <span class="icon">
                                  <i class="fa-solid fa-address-card"></i>
                                </span>
                                  <span>Faire le test</span>
                              </button>
                          </div>
                      </article>
                      <article class="tile is-child notification is-warning">
                          <p class="title logo-text">
                              <Logo color={"000000"} />
                          </p>
                          <p>A travers la saisie d’un questionnaire (Kolb) nous cherchons à déterminer un profil d’apprenant dans le projet DataTrainx. L’utilisateur sera enregistré en vidéo et une comparaison sera effectuée avec les émotions que vous aurez exprimées.</p>
                          <div class="buttons">
                              <button class="button are-medium right is-warning is-light" on:click={() => animateScroll.scrollTo({element: "#article"})}>
                                <span class="icon">
                                    <i class="fa-solid fa-circle-info"></i>
                                </span>
                                  <span>En savoir plus</span>
                              </button>
                          </div>
                      </article>
                  </div>
                  <div class="tile is-parent">
                      <article class="tile is-child notification is-info">
                          <p class="title">Capture vidéo</p>
                          <p class="subtitle">Prêt à capturer vos émotions ?</p>
                          <Faceapi/>
                      </article>
                  </div>
              </div>
              <div class="tile is-parent">
                  <article class="tile is-child notification is-danger">
                      <p class="title">Protection de votre image</p>
                      <p class="">Des données collectés uniquement à des fins de recherche en partenariat avec l'IPST CNAM de l'université de Toulouse. DataTrainX est un projet d'étude personnel dans le cadre de mon mémoire d'ingénieur. Les données sont collectés sur mon propre serveur, il n'y a aucun autre intermédiaire et les données transitent de manière cryptée!<br>Les données de resultats sont anonymisées et disponibles en <span class="link" on:click ={() => layoutStore.setLayout("opendata")}>OpenData</span>.</p>
                  </article>
              </div>
          </div>
          <div class="tile is-parent is-vertical">
              <article class="tile is-child notification is-success">
                  <div class="content">
                      <p class="title">Réseau neuronal convolutif</p>
                      <div class="content">
                          <p>En apprentissage automatique, un réseau de neurones convolutifs, appellé aussi CNN, est un type de réseau de neurones artificiels, dans lequel le motif de connexion entre les neurones est inspiré par le cortex visuel des animaux. Les neurones de cette région du cerveau sont arrangés de sorte qu'ils correspondent à des régions qui se chevauchent lors du pavage du champ visuel.</p>
                          <p>Leur fonctionnement est inspiré par les processus biologiques, ils consistent en un empilage multicouche de perceptrons, dont le but est de prétraiter de petites quantités d'informations.</p>
                          <p>Les réseaux neuronaux convolutifs ont de larges applications dans la reconnaissance d'image et vidéo, les systèmes de recommandation et le traitement du langage naturel.</p>
                          <button class="button is-primary" id="explain-button" on:click ={() => layoutStore.setLayout("cnn")}>
                            <span class="icon">
                              <i class="fas fa-eye"></i>
                            </span>
                              <span>Comment ça marche ?</span>
                          </button>
                      </div>
                  </div>
              </article>
          </div>
      </div>
  </div>





