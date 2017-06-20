<template>
  <div class="col-sm-4 col-sm-offset-4">
    <h3>UPLOAD</h3>
   <input name="photo" type ="file" @change="oneFileChange" cature accept="image/*">
	 	<button class="btn btn-primary" @click="submit">Save File</button>
  </div>


</template>

<script>
  export default {

    data() {
      return {
       imgFile: null,
			 form: new FormData (), // formualer hecho para upload files
			 reader: new FileReader(), // permet que el archivo fisico enviarlo por post 
      }
    },

    methods: {
			oneFileChange(e){
				console.log(e);
				this.imgFile = e.target.files[0];
				console.log(this.imgFile);
				this.reader.readAsDataURL(this.imgFile);
				console.log(this.reader);
			},
			submit(){
				this.form.append('photo', this.imgFile);
				this.$http.post('http://localhost:3000/uploading',this.form).then((res) => {
					this.$toasted.show('Uploaded!').goAway(1500);
				}, (err) => {
					this.$toasted.show(err).goAway(1500);
				})
			}

				



			}
     
    }

  
</script>