<script setup>  
  const props = defineProps({
    graphData: Object,
    sources: Object,
  })
</script>

<script>
  export function closeModal() {
    document.getElementById('graphSettings').close()
  }
</script>

<template>
    <dialog class="favDialog" id="graphSettings">
      <div class="modal-header d-flex flex-row justify-content-between position-relative">
        <h3 class="">Graph Settings</h3>
        <span class="pointer position-absolute top-0 end-0" :onclick="closeModal">
          <svg xmlns="http://www.w3.org/2000/svg" width="32" height="32" fill="currentColor" class="bi bi-x" viewBox="0 0 16 16">
            <path d="M4.646 4.646a.5.5 0 0 1 .708 0L8 7.293l2.646-2.647a.5.5 0 0 1 .708.708L8.707 8l2.647 2.646a.5.5 0 0 1-.708.708L8 8.707l-2.646 2.647a.5.5 0 0 1-.708-.708L7.293 8 4.646 5.354a.5.5 0 0 1 0-.708z"/>
          </svg>
        </span>
      </div>

      <hr>
        <form id="contactForm" class="container">
          <div class="form-group row">
            <div class="form-floating mb-3">
                <input class="form-control" id="title" type="text" placeholder="title" v-model="graphData.title" data-sb-validations="" />
                <label class="ms-2" for="title">title</label>
            </div>
          </div>
          <div class="input-group mb-3">
            <label class="input-group-text m-0" for="source">data source</label>
            <select class="form-select" id="source" v-model="graphData.dataRecord.source">
              <option v-for="source in sources" :value="source">{{ source.name }}</option>
            </select>
          </div>
          <div class="form-group row">
            <div class="form-floating mb-3 col-6">
                <input class="form-control" id="xmin" type="text" placeholder="Xmin" v-model="graphData.Xmin" data-sb-validations="" />
                <label class="ms-2" for="xmin">Xmin</label>
            </div>
            <div class="form-floating mb-3 col-6">
                <input class="form-control" id="xmax" type="text" placeholder="Xmax" v-model="graphData.Xmax" data-sb-validations="" />
                <label class="ms-2" for="xmax">Xmax</label>
            </div>
          </div>
          <div class="form-group row">
            <div class="form-floating mb-3 col-6">
                <input class="form-control" id="Ymin" type="text" placeholder="Ymin" v-model="graphData.Ymin" data-sb-validations="" />
                <label class="ms-2" for="Ymin">Ymin</label>
            </div>
            <div class="form-floating mb-3 col-6">
                <input class="form-control" id="Ymax" type="text" placeholder="Ymax" v-model="graphData.Ymax" data-sb-validations="" />
                <label class="ms-2" for="Ymax">Ymax</label>
            </div>
          </div>
          <div class="form-group row">
            <div class="form-floating mb-3 col-6">
                <input class="form-control" id="lineColor" type="text" placeholder="lineColor" v-model="graphData.lineColor" data-sb-validations="" />
                <label class="ms-2" for="lineColor">lineColor</label>
            </div>
            <div class="form-floating mb-3 col-6">
                <input class="form-control" id="fillColor" type="text" placeholder="fillColor" v-model="graphData.fillColor" data-sb-validations="" />
                <label class="ms-2" for="fillColor">fillColor</label>
            </div>
          </div>
          <div class="form-group row">
            <div class="form-floating mb-3 col-6">
                <input class="form-control" id="Xunit" type="text" placeholder="Xunit" v-model="graphData.Xunit" data-sb-validations="" />
                <label class="ms-2" for="Xunit">Xunit</label>
            </div>
            <div class="form-floating mb-3 col-6">
                <input class="form-control" id="Yunit" type="text" placeholder="Yunit" v-model="graphData.Yunit" data-sb-validations="" />
                <label class="ms-2" for="Yunit">Yunit</label>
            </div>
          </div>
        </form>

      <div class="modal-footer d-flex flex-row justify-content-around mt-3">
        <button class="btn btn-secondary" value="cancel" @click="closeModal">Fermer</button>
      </div>
    </dialog>
</template>

<style scoped>
  dialog {
    position: fixed;
    top:50%;
    left:50%;
    transform: translate(-50%, -50%);
    z-index: 100;
    padding: 50px;
    border-radius: 5px;
    background-color: #ecf0f1;
  }

  dialog::backdrop {
    background-color: rgba(0,0,0,0.6);
  }

  label:nth-child(3) {
    margin-left: 10px;
  }

  label:first-child {
    margin-left: -10px;
  }

</style>