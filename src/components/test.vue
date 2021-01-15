<template>
  <div>
      <canvas id="gameCanvas" style="height: 100%; width: 100%"></canvas>
  </div>
</template>

<script>
  import * as BABYLON from 'babylonjs';
  import 'babylonjs-loaders';
  import dummy3 from 'file-loader!@/assets/mc-laren/source/McLaren.glb';

  export default {
    data() {
      return {

      };
    },
    methods: {
      init() {
        const _this = this
        this.canvas = document.getElementById('gameCanvas')
        this.engine = new BABYLON.Engine(this.canvas, true)
        this.scene = new BABYLON.Scene(this.engine)
        this.camera = new BABYLON.FreeCamera('camera1', new BABYLON.Vector3(0, 5,-10), this.scene);
        this.camera.setTarget(BABYLON.Vector3.Zero());
        this.light = new BABYLON.HemisphericLight('light1', new BABYLON.Vector3(0,1,0), this.scene)
        this.box = new BABYLON.Mesh.CreateBox('box1', 2.0, this.scene)
        this.texture = new BABYLON.StandardMaterial("texture1", this.scene);
        this.texture.bumpTexture = new BABYLON.Texture("../assets/logo.png", this.scene);
        this.box.material = this.texture;
        this.animationX = new BABYLON.Animation.CreateAndStartAnimation('boxrotate', this.box, 'rotation.x', 10, 360, 1, 10);
        this.animationY = new BABYLON.Animation.CreateAndStartAnimation('boxrotate', this.box, 'rotation.y', 10, 360, 1, 10);   
        this.engine.runRenderLoop(function(){
            _this.scene.render();
        });
      }
      
    },
    mounted() {
      console.log("test")
      this.init()
    },


  }
</script>

<style lang="scss" scoped>

</style>