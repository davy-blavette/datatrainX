<script>
    import Activist from "./Activist.svelte";
    import Pragmatist from "./Pragmatist.svelte";
    export let pragmatist;
    export let activist;
</script>
<div class="">
    <p>Les apprenants qui ont une préférence pour ce style d’apprentissage apprennent facilement lorsqu’ils peuvent vivre des expériences pratiques et des activités concrètes. Ils tirent leur apprentissage en agissant et par les émotions/sentiments qu’ils ressentent durant les premières phases de l’apprentissage. Ainsi, l’adaptateur aura de fortes aptitudes à s’ajuster aux situations qu’il rencontre en prenant des décisions rapides en fonction des circonstances. Il aura tendance à résoudre les problèmes en se fiant à son intuition et aux informations qu’il pourra obtenir des autres personnes, plutôt qu’en procédant à une analyse rationnelle et systématique de la situation. Enfin, l’adaptateur est sensible aux opinions et aux réactions des autres et en tient compte pour juger de ses actions.</p>
    <p class="subtitle">Implications pour la formation en organisation :</p>
    <p>Pour répondre à ce style d’apprentissage, une formation doit recourir à des méthodes et techniques d’enseignement qui favorisent l’expérimentation et l’application des nouvelles connaissances. Les mises en situation, les jeux de rôles sont au nombre des activités pratiques à utiliser.</p>
    <hr>
    <Pragmatist
            score={pragmatist}
    />
    <Activist
            score={activist}
    />
</div>