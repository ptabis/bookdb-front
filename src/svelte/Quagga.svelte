<script>
  import { createEventDispatcher } from "svelte";
  import Quagga from "quagga";
  import { quaggaClosed } from "../stores/quaggaStore.js";

  let dispatch = createEventDispatcher();
  let devices = [];
  let selectedDevice;
  let closed = 1;

  quaggaClosed.subscribe(value => {
    if (closed != value) {
      if (value == 0) init();
      else close();
    }
  })
  async function _populateCameraDevices() {
    let videoDevices = await Quagga.CameraAccess.enumerateVideoDevices(),
      selectedDeviceLabel = Quagga.CameraAccess.getActiveStreamLabel();
    devices = videoDevices.map(({ id, deviceId, label }) => ({
      id: id || deviceId,
      label: label || id || deviceId
    }));
    selectedDeviceLabel = devices.find(
      dev => dev.label === selectedDeviceLabel
    );
  }

  async function init() {
    closed = 0;
    Quagga.init(
      {
        inputStream: {
          name: "Live",
          type: "LiveStream",
          target: document.querySelector("#scannerPreview"),
          constraints: {
            width: 640,
            height: 480,
            facingMode: "environment"
          },
          singleChannel: false
        },
        decoder: {
          readers: ["ean_reader"],
          multiple: false
        },
        numOfWorkers: 4,
        frequency: 10,
        debug: false
      },
      function(err) {
        if (err) {
          console.log(err);
          return;
        }
        _populateCameraDevices();
        Quagga.start();
      }
    );

    Quagga.onDetected(result => {
      let foundEan = result.codeResult.code;
      // Quagga.stop();
      console.log(`Found EAN: ${foundEan}`);
      setTimeout(() =>
        dispatch("ean", {
          ean: foundEan,
          imageSrc: Quagga.canvas.dom.image.toDataURL()
        })
      );
    });
  }
  function close() {
    Quagga.stop();
    closed = 1;
  }
</script>

<style>
  .wrap {
    text-align: center;
  }
  #scannerPreview {
    position: relative;
  }
  :global(#scannerPreview > *) {
    max-width: 100% !important;
  }
  :global(#scannerPreview canvas) {
    position: absolute;
    top: 0;
    left: 0;
  }
</style>

<div class="wrap" style="display: {closed ? 'none' : 'block'};">
  <div id="scannerPreview" />
</div>
