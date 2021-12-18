<template>

<body class="hold-transition sidebar-mini layout-fixed">
      <!-- Google Font: Source Sans Pro -->
  <!-- <link rel="stylesheet" href="https://fonts.googleapis.com/css?family=Source+Sans+Pro:300,400,400i,700&display=fallback"> -->
  <!-- Font Awesome -->
  <link rel="stylesheet" href="../../plugins/fontawesome-free/css/all.min.css">
  <!-- Ionicons -->
  <!-- <link rel="stylesheet" href="https://code.ionicframework.com/ionicons/2.0.1/css/ionicons.min.css"> -->
  <!-- Tempusdominus Bootstrap 4 -->
  <link rel="stylesheet" href="../../plugins/tempusdominus-bootstrap-4/css/tempusdominus-bootstrap-4.min.css">
  <!-- iCheck -->
  <link rel="stylesheet" href="../../plugins/icheck-bootstrap/icheck-bootstrap.min.css">
  <!-- JQVMap -->
  <link rel="stylesheet" href="../../plugins/jqvmap/jqvmap.min.css">
  <!-- Theme style -->
  <link rel="stylesheet" href="../../dist/css/adminlte.min.css">
  <!-- overlayScrollbars -->
  <link rel="stylesheet" href="../../plugins/overlayScrollbars/css/OverlayScrollbars.min.css">
  <!-- Daterange picker -->
  <link rel="stylesheet" href="../../plugins/daterangepicker/daterangepicker.css">
  <!-- summernote -->
  <link rel="stylesheet" href="../../plugins/summernote/summernote-bs4.min.css">
<div class="wrapper">

  <!-- Preloader -->
  <div class="preloader flex-column justify-content-center align-items-center">
    <img class="animation__shake" src="../../dist/img/AdminLTELogo.png" alt="AdminLTELogo" height="60" width="60">
  </div>
  <!-- /.navbar -->

  <!-- Main Sidebar Container -->
  <aside class="main-sidebar sidebar-dark   levation-4">
    <!-- Brand Logo -->
    <a href="index3.html" class="brand-link" style="background-color: #07996d">
      <img src="../../dist/img/logo.png" alt="AdminLTE Logo" class="brand-image img-circle elevation-3" style="opacity: .8">
      <span class="brand-text font-weight-light">AGITEL </span>
    </a>

    <!-- Sidebar -->
    <div class="sidebar" style="background-color: #07996d">
      <!-- Sidebar user panel (optional) -->
      <div class="user-panel mt-3 pb-3 mb-3 d-flex">
        <div class="image">
          <img src="../../dist/img/user2-160x160.jpg" class="img-circle elevation-2" alt="User Image">
        </div>
        <div class="info">
          <a href="#" class="d-block" style="color:white">Admin</a>
        </div>
      </div>


      <!-- Sidebar Menu -->
      <nav class="mt-2">
        <ul class="nav nav-pills nav-sidebar flex-column" data-widget="treeview" role="menu" data-accordion="false">
          <!-- Add icons to the links using the .nav-icon class
               with font-awesome or any other icon font library -->
          <li class="nav-item">
            <a href="pages/widgets.html" class="nav-link" style="color:white">
              <p>
                Liste des étudiants
                <span class="right badge badge-danger">{{nbEtudiantEnCours}}</span>
              </p>
            </a>
          </li>
        </ul>
      </nav>
      <!-- /.sidebar-menu -->
    </div>
    <!-- /.sidebar -->
  </aside>

  <!-- Content Wrapper. Contains page content -->
  <div class="content-wrapper">
    <!-- Content Header (Page header) -->
    <section class="content-header">
      <div class="container-fluid">
        <div class="row mb-2">
          <div class="col-sm-6">
            <h1>listes etudiants</h1>
          </div>
          <div class="col-sm-6">
            <ol class="breadcrumb float-sm-right">
              <li class="breadcrumb-item active">liste Etudiants</li>
            </ol>
          </div>
        </div>
      </div><!-- /.container-fluid -->
    </section>

    <!-- Main content -->
    <section class="content">
      <div class="container-fluid">
        <div class="row">
          <div class="col-12">
            <!-- /.card -->
            <div class="card">
              <div class="card-header">
                <h3 class="card-title">Liste des etudiants</h3>
              </div>
              <!-- /.card-header -->
              <div class="card-body">
                <table id="example1" class="table table-bordered table-striped">
                  <thead>
                  <tr>
                    <th>Photo</th>
                    <th>Nom</th>
                    <th>Prenom</th>
                    <th>matricule</th>
                    <th>cni</th>
                    <th>bac</th>
                    <th>statut</th>
                    <th>action</th>
                  </tr>
                  </thead>
                  <tbody>
                  <tr v-for ="(etudiant,index) in etudiants" :key="index">
                    <td> 
                      <img v-if="etudiant.photo != ''" :src="'http://localhost:8000'+etudiant.photo" width="100" height="100" alt="">
                      <img v-if="etudiant.photo == ''" src="../../dist/img/avatar.png" width="100" height="100" alt="">
                    </td>
                    <td>{{ etudiant.username}}</td>
                    <td>{{ etudiant.prenom}}</td>
                    <td>{{ etudiant.matricule}}</td>
                    <td>
                     <button type="button" class="btn btn-default" data-toggle="modal" data-target="#bmodal-default" @click="Afficher(etudiant.id)"> 
                      <img :src="'http://localhost:8000'+etudiant.cni" width="100" height="100" alt="">
                      </button>   
                    </td>
                    <td>
                     <button type="button" class="btn btn-default" data-toggle="modal" data-target="#amodal-default" @click="Afficher(etudiant.id)"> 
                       <img :src="'http://localhost:8000'+etudiant.bacBenef" width="100" height="100" alt="">
                      </button>   
                    </td>
                    <td>
                      {{ etudiant.statutBenef}}
                                      <!-- <button type="button" class="btn btn-outline-primary" data-bs-toggle="modal" data-bs-target="#Modifier" >Modifier</button> -->
                    </td>
                    <td>
                    <button type="button" class="btn btn-default" data-toggle="modal" data-target="#modal-default" @click="Modifier(etudiant.id)">
                      Details
                    </button>
                    </td>
                      <!-- /.control-sidebar -->

                  </tr>
                  </tbody>
                  <tfoot>
                  <tr>
                    <th>Photo</th>
                    <th>Nom</th>
                    <th>Prenom</th>
                    <th>matricule</th>
                    <th>cni</th>
                    <th>bac</th>
                    <th>statut</th>
                    <th>action</th>
                  </tr>
                  </tfoot>
                </table>
              </div>
              <!-- /.card-body -->
            </div>
            <!-- /.card -->
          </div>
          <!-- /.col -->
        </div>
        <!-- /.row -->
      </div>
      <!-- /.container-fluid -->
    </section>
    <!-- /.content -->
  </div>
  <!-- /.content-wrapper -->
  <footer class="main-footer">
    <strong>Copyright &copy; 2021-2022 <a href="https://adminlte.io">AGITEL FORMATION</a>.</strong>
    Tous les droits sont réservés.
    <div class="float-right d-none d-sm-inline-block">
      <b>Version</b> 3.2.0-rc
    </div>
  </footer>

  <!-- Control Sidebar -->
  <aside class="control-sidebar control-sidebar-dark">
    <!-- Control sidebar content goes here -->
  </aside>

  
        <ModifierEtudiants
        :idd="idEtudiant"
        :etudiant="etudiant"/>
        <AfficherBac
        :idd="idEtudiant"
        :etudiant="etudiant"/>
        <AfficherCni
        :idd="idEtudiant"
        :etudiant="etudiant"/>
</div>
<!-- ./wrapper -->

</body>

</template>

<script>
import axios from 'axios';
import ModifierEtudiants from '../components/Modals/ModifierEtudiants.vue';
import AfficherBac from '../components/Modals/AfficherBac.vue';
import AfficherCni from '../components/Modals/AfficherCni.vue';

export default {
    name : 'DashBoard',
        data() {
        return {
                etudiants : [],
                idEtudiant:'',
                etudiant:{},
                nbEtudiantEnCours:0
        }
    },
       methods : {
            async getDatas (){
                console.log(axios.get("http://localhost:8000/api/etudiants"));
                await axios
                .get("http://localhost:8000/api/etudiants")
                .then(response=> {
                    console.log(response);
                    for (const etudiant of response.data){
                        this.etudiants.push(etudiant)
                    }
                    for(const nb of this.etudiants)
                    {
                      if(nb.statutBenef =="en cours") 
                      this.nbEtudiantEnCours = this.nbEtudiantEnCours + 1;
                    }
                    console.log(this.nbEtudiantEnCours);
                console.log(this.admins);
            });
            },
            Modifier(val){
                // this.maj =true;
                this.idEtudiant = val;
                // console.log(val);
                axios
                .get('http://localhost:8000/api/etudiants/'+val)
                .then(response =>{
                    this.etudiant  = response.data;
                });
            },
            Afficher(val){
                // this.maj =true;
                this.idEtudiant = val;
                // console.log(val);
                axios
                .get('http://localhost:8000/api/etudiants/'+val)
                .then(response =>{
                    this.etudiant  = response.data;
                });
            },
            // goToDash() {
            //     console.log('appuyer');
            //     this.admins.forEach(etudiant => {
            //         if(etudiant.email == this.username && etudiant.password == this.password)
            //         {
            //             console.log('succ');
            //             this.$router.push('/DashBoard');
            //         }else
            //         {
            //             console.log("error");
            //         }
            //     });
            // }
        },
    async mounted() {
        await this.getDatas();
        console.log('ok')
    },
  components :{
    ModifierEtudiants,
    AfficherBac,
    AfficherCni
}
}
</script>

<style>

</style>
