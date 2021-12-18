<template>
      <div class="modal fade" id="modal-default">
        <div class="modal-dialog">
          <div class="modal-content">
            <div class="modal-header">
              <h4 class="modal-title">Detail etudiant <b style="color: #07996d">{{etudiant.username}} </b> </h4>
              <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                <span aria-hidden="true">&times;</span>
              </button>
            </div>
            <div class="modal-body">
                <img :src="'http://localhost:8000'+etudiant.photo" width="200" height="200" alt="" style="border-radius: 50%; margin-left:30%">
                <table style=" margin-left:20%">
                        <tr>
                            <td>Nom :</td>
                            <td>{{etudiant.username}}</td>
                        </tr>
                        <tr>
                            <td>prenom :</td>
                            <td>{{ etudiant.prenom}}</td>
                        </tr>
                        <tr>
                            <td>email :</td>
                            <td>{{ etudiant.email}}</td>
                        </tr>
                        <tr>
                            <td>filiere :</td>
                            <td>{{ etudiant.filiere}}</td>
                        </tr>
                        <tr>
                            <td>niveau :</td>
                            <td>{{ etudiant.niveau}}</td>
                        </tr>
                        <tr>
                            <td>Matricule :</td>
                            <td>{{ etudiant.matricule}}</td>
                        </tr>
                        <tr>
                            <td> Sexe : </td>
                            <td>{{ etudiant.sexe}}</td>
                        </tr>
                        <tr>
                            <td>Date de naissance  :</td>
                            <td>{{ formatDate(etudiant.dateNaissance)}}</td>       
                        </tr>
                        <tr>
                            <td>lieu de naissance :</td>
                            <td>{{ etudiant.lieuNaissance}}</td>               
                        </tr>
                        <tr>
                            <td>tel etudiant :</td>
                            <td>{{ etudiant.telEtudiant}}</td>                 
                        </tr>
                        <tr>
                            <td>tel parent :</td>
                            <td>{{ etudiant.telParent}}</td>                
                        </tr>
                        <tr>
                            <td>Statut : </td> 
                            <td>
                                {{etudiant.statutBenef}}
                            <select name="" id="" v-model="etudiant.statutBenef">
                                <option v-if="etudiant.statutBenef == 'en cours'" value="acceptable">Acceptable</option>
                                <option value="actif">Actif</option>
                                <option value="inactif">Inactif</option>
                            </select>
                            </td>
                        </tr>
                </table>
            </div>
            <div class="modal-footer justify-content-between">
              <button type="button" class="btn btn-default" data-dismiss="modal">Fermer</button>
              <button type="button" class="btn btn-primary" @click="ModifierFournisseur" >Enregistrer</button>
            </div>
          </div>
          <!-- /.modal-content -->
        </div>
        <!-- /.modal-dialog -->
      </div>
</template>

<script>
import  axios from 'axios'
import moment from 'moment'
export default {
    data(){
        return{
            nom:'',
            station:'',
            numero :'',
        }
    },
    props : ['idd','etudiant'],
    methods : {
        ModifierFournisseur(){
                const options = {
                    url: 'http://localhost:8000/api/etudiants/'+this.idd,
                    method: 'PUT',
                    headers: {
                        'Accept': 'application/json',
                        'Content-Type': 'application/json;charset=UTF-8'
                },
                data: {
                        statutBenef: this.etudiant.statutBenef
                    }
                };
                axios(options)
                .then( response =>{
                    if(response != null){
                        this.$notify({
                            title: "Success",
                            text: "statut modifié",
                            type : "success"
                        })
                    }
                this.$emit("on-reload",true)
                })
                .catch(error =>{
                    this.$notify({
                        title: "Erreur",
                        text: error.message,
                        type : "error"
                    })
                })
        },
        formatDate(dateString) {
            if (dateString) {
            return moment(String(dateString)).format('DD/MM/YYYY')
            }
        }
    },
}
</script>

<style>

</style>