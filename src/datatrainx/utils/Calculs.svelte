<script>
    import {getTrainer, updatePush} from "../../service-factory/crud";
    import {
        baseUrl,
        chartExpressions,
        dataProfil, kolbProfil, preferenceProfil,
        resultatExpressions, scoreTab,
        streamExpression
    } from "../../service-factory/data";
    import {infoLoadStore, kolbStore, layoutStore, userIdtStore, userTokenStore} from "../../stores";
    import {onMount} from "svelte";
    import Loading from "./Loading.svelte";
    import LogoHead from "../layout/LogoHead.svelte";
    import {questions} from "../../service-factory/kolb2";

    infoLoadStore.set("Calcul des resultats...");

    let jsonTrainer = [];
    let data;
    let userId;
    let Break = {};
    let token;
    userIdtStore.subscribe(value => {
        userId = value;
    });
    userTokenStore.subscribe(value => {
        token = value;
    });
    function updateProfil() {

        onMount(async () => {
            let method = "GET";
            URL = `${baseUrl}/dataProfil/${userId}`;
            const res = await fetch(URL, {
                method,
                headers: {
                    "Content-Type": "application/json",
                    "Authorization":`Bearer ${token}`
                }
            });
            jsonTrainer = [await res.json()];
            data = Object.values(jsonTrainer)[0];
            preferences();
            scoreProfil();
            profile();
            emotions();
            await updatePush('dataProfil', {
                apprenant: dataProfil.apprenant,
                expressions: dataProfil.expressions,
                created: Date.now()
            });
        });

        kolbStore.set(questions.length);
    }


    function preferences() {

        let score = 0;
        let totalScore = 0;
        for (const [profil, value] of Object.entries(data.dataProfil.apprenant.dim1)) {
            try {
                Object.entries(preferenceProfil[profil]).forEach(([type, forceValue], index) => {
                    if (value.scoreRacine >= forceValue) {
                        dataProfil.apprenant.dim1[profil].tab = scoreTab[index].tab;
                        score = scoreTab[index].score;
                        totalScore += score;
                        throw Break;
                    }
                });
            } catch (e) {
                dataProfil.apprenant.dim1[profil].scoreRacine = value.scoreRacine;
                dataProfil.apprenant.dim1[profil].score = score;
            }
        }
        dataProfil.apprenant.score = Math.round(totalScore / Object.keys(data.dataProfil.apprenant.dim1).length);

    }

    function profile() {
        let bestProfil = "";
        let bestScore = 0;
        for (const [profil, score] of Object.entries(dataProfil.apprenant.dim2)) {
            if (score > bestScore) {
                bestProfil = profil.toUpperCase();
                bestScore = score;
            } else if (score == bestScore) {
                bestProfil += "/" + profil.toUpperCase();
            }
        }
        dataProfil.apprenant.profil = bestProfil;

    }

    function scoreProfil() {
        let score = 0;
        for (const [profil, array] of Object.entries(kolbProfil)) {
            score = dataProfil.apprenant.dim1[array[0]].score + dataProfil.apprenant.dim1[array[1]].score;
            dataProfil.apprenant.dim2[profil] = Math.trunc(score / 2);
        }
    }

    function emotions() {

        let counter = 0;
        let totalCounter = 0;
        //clean value
        for (const [expression, value] of Object.entries(chartExpressions)) {
            streamExpression[expression].length = 0;
        }

        //boucle sur les expressions streaming de la collection trainer
        data.dataExpression.forEach(function (expressions) {
            //boucle sur le panel d'expression de la collection trainer
            for (const [expression, value] of Object.entries(expressions.FaceExpression)) {
                //on ne souhaite pas faire de statistiques sur l'expression neutre
                if (value > 0 && expression != 'neutre') {
                    //on ajoute au serviceFactory de dataProfil
                    resultatExpressions[expression].count += 1;
                    resultatExpressions[expression].total += value;
                    if (resultatExpressions[expression].best < value) {
                        resultatExpressions[expression].best = value;
                        resultatExpressions[expression].image = expressions.FaceDetection.image;
                        resultatExpressions[expression].key = counter;
                    }
                    //serviceFactory temporaire utiliser juste pour l'affichage des resultats
                    streamExpression[expression].push({
                        x: expressions.created,
                        y: value,
                    });
                    counter++;
                }
                ;
                totalCounter++;
            }
        });
        //ratio
        for (const [expression, value] of Object.entries(resultatExpressions)) {
            resultatExpressions[expression].ratio = Math.round(resultatExpressions[expression].count / counter * 100);
        };
        dataProfil.expressions.resultatExpressions = resultatExpressions;
        dataProfil.expressions.score = Math.round(counter / totalCounter * 100);
    }

    updateProfil();

</script>
<section class="container has-text-centered">
    {#if jsonTrainer.length === 0}
        <Loading />
    {:else}
        <div class="tile">
            <LogoHead/>
        </div>
        <div class="subtitle">
            <button class="button are-medium center is-success is-rounded" on:click ={() => layoutStore.setLayout("resultatKolb")}>
                <span class="icon">
                    <i class="fa-solid fa-check"></i>
                </span>
                <span>Voir les résultats</span>
            </button>
        </div>
    {/if}
</section>