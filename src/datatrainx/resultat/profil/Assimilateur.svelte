<script>
    import Therorist from "./Therorist.svelte";
    import Reflector from "./Reflector.svelte";
    export let reflector;
    export let theorist;
</script>
<div class="">
    <p>Les apprenants qui ont une préférence pour ce style d’apprentissage vont avoir une forte capacité d’assimilation et de synthèse de l’information. Elles vont privilégier la théorie à la pratique et vont aimer comprendre la dynamique de causalité d’une situation. Leurs caractéristiques résultent de leurs affinités avec la conceptualisation abstraite et l’observation réfléchie. Travaillant davantage en solitaire, l’assimilateur excelle dans le raisonnement inductif et dans l’intégration d’observations disparates. Il aimera résoudre des problèmes complexes qui impliquent un grand nombre de facteurs et de dimensions en modélisant la situation.</p>
    <p class="subtitle">Implications pour la formation en organisation :</p>
    <p>Pour répondre à ce style d’apprentissage, une formation doit inclure des notions théoriques. Les études de cas et la gestion de projets complexes permettant l’assimilation des apprentissages sont au nombre des activités pouvant être utilisées.</p>
    <hr>
    <Therorist
            score={theorist}
    />
    <Reflector
            score={reflector}
    />
</div>