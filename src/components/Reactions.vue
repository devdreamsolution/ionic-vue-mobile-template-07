
<template>
	<ion-buttons class="reactions">
		<ion-button @click="likeFn">
			<ion-icon :icon="heart"></ion-icon>
		</ion-button>
		<ion-button @click="openModal()">
			<ion-icon :icon="addCircle"></ion-icon>
		</ion-button>
	</ion-buttons>
</template>

<script>
import {
  IonButtons,
  IonButton,
  IonIcon,
  modalController,
} from "@ionic/vue";

import Modal from "./Modal";

import { 
  addCircle, 
  heart 
} from "ionicons/icons";

export default {
	name: "Reactions",
  props: {
    likePost: {
      type: Boolean,
      required: true,
      default: false,
    },
  },
  components: {
    IonIcon,
    IonButton,
    IonButtons
	},
  setup() {
    return {
      addCircle,
      heart
    };
  },
  methods: {
    likeFn() {
			this.$emit("likeClick", !this.likePost);
    },
    async openModal(ticket) {
    const modalInstance = modalController;
    const modal = await modalInstance
      .create({
        component: Modal,
        componentProps: {
          context: this,
          data: ticket,
          modalInstance,
        },
      })

    return modal.present();
  },
  }
};
</script>

<style lang="scss" scoped>
ion-modal { padding-top: 80%; }
.reactions {
  float: right;
  color: #fff;
  ion-button, button {
    margin: 0;
    padding: 0;
  }
}
</style>
  