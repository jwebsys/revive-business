<template>
  <section class="section-shaped my-0">
    <div class="shape shape-style-1 bg-gradient-warning">
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
      <span></span>
    </div>

    <div class="container pt-lg-md">
      <div class="row">
        <div class="col-md-3 row ml-0">
          <base-button
            icon="fa fa-home"
            class="mb-5 text-warning text-capitalize"
            type="white"
            @click="$router.push('/')"
          ></base-button>
          <base-button
            icon="ni ni-bold-left"
            class="mb-5 text-warning text-capitalize"
            type="white"
            @click="$router.go(-1)"
          >{{$t("Voltar")}}</base-button>
        </div>
      </div>

      <div class="row justify-content-center">
        <div class="col-lg-12">
          <div class="row row-grid">
            <div v-for="(solucao, index) in $t('investimentos/Dashboard.solucoes')" :key="index" class="col-lg-4 mb-5">
              <card class="border-0" shadow body-classes="py-5">
                <div class="row" style="margin-left: 1px">
                  <icon :name="solucao.icone" gradient="warning" color="white" shadow rounded></icon>
                  <h4
                    style="margin-top: 10px; margin-left: 20px"
                    class="text-default"
                  >{{$t("investimentos/Dashboard.solucoes["+index+"].titulo")}}</h4>
                </div>
                <p class="mt-3">{{$t("investimentos/Dashboard.solucoes["+index+"].descricao")}}</p>
                <div class="text-center">
                  <base-button
                    class="my-4"
                    type="warning text-capitalize"
                    style="font-size: 16px"
                    @click="modal(index)"
                  >{{$t("investimentos/Dashboard.solucoes["+index+"].botao")}}</base-button>
                </div>
              </card>
            </div>
          </div>
        </div>
      </div>
    </div>
    <modal
      :show.sync="modal_visivel"
      gradient="warning"
      modal-classes="modal-danger modal-dialog-centered"
    >
      <h4
        slot="header"
        class="modal-title"
        id="modal-title-notification"
      >{{$t("investimentos/Dashboard.solucoes["+index_modal+"].titulo")}}</h4>

      <div>
        <h5
          class="text-white mt-4"
        >{{$t("investimentos/Dashboard.solucoes["+index_modal+"].texto_modal_secundario")}}</h5>
        <p
          v-if="solucoes[index_modal].texto_modal_alerta"
          class="text-white mt-4"
        >{{solucoes[index_modal].texto_modal_alerta}}</p>
        <p class="mt-4">
          {{$t("investimentos/Dashboard.complemento.modal.informacoes")}}
          <br />(85) 99705 - 4321
        </p>
      </div>
      <template slot="footer">
        <base-button
          type="white"
          text-color="warning"
          class="text-capitalize"
          @click="modal_router()"
        >{{$t("investimentos/Dashboard.complemento.modal.ideias_b")}}</base-button>
      </template>
    </modal>
  </section>
</template>

<script>
import Modal from "@/components/Modal.vue";
export default {
  components: {
    Modal
  },
  data() {
    return {
      modal_visivel: false,
      index_modal: 0,
      solucoes: this.$t("investimentos/Dashboard.solucoes"),
    };
  },
  methods: {
    modal(i) {
      this.index_modal = i;
      this.modal_visivel = true;
    },

    async modal_router() {
      this.fechar_modal().then(() => this.$router.push("solucoes_lista"));
      //Foi necessário utilizar força bruta, pois o await não funcionou.
    },

    async fechar_modal() {
      this.modal_visivel = await false;
      return;
    }
  }
};
</script>
