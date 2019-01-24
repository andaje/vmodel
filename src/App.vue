<template>
  <div id="app">
      <div class="container">
          <div class="row">
              <div class="col">
                  <div class="card">
                      <h4 class="card-header" :class="cardClasses">
                      Class Binding
                        </h4>
                      <div class="card-body">
                          <div class="form-group">
                              <select class="form-control" v-model="card.selectedStyling">
                                  <option v-for="style in card.contextualStyles" :value="style">
                                      {{ style.type | ucfirst }}
                                  </option>
                              </select>
                          </div>
                      </div>
                  </div>
              </div>
              <div class="col">
                  <div class="card">
                      <h4 class="card-header">
                          Binding Style
                      </h4>
                      <div class="card-body">
                          <div class="form-group">
                              <div class="input-group">
                                  <input class="form-control" v-model="progress.width"
                                         placeholder="breedte progressbar in pct" type="text">
                                  <span class="input-group-addon">%</span>
                              </div>
                          </div>
                          <div class="form-group">
                              <input class="form-control" v-model="progress.backgroundcolor" type="text">
                          </div>
                      </div>
                      <div class="card-footer">
                          <div class="progress">
                              <div class="progress-bar" :style="progressStyling">
                              
                              </div>
                          </div>
                      </div>
                  </div>
              </div>
          </div>
      </div>
  </div>
</template>

<script>


export default {
    /* applicatie naam */
  name: 'app',
    /* view model die door App.vue wordt gebruikt*/
    /* @returns {object} van het view-model retourneren*/
  data(){
      return{
          /**card**/
          card:{
              selectedStyling:{
                  type:'light',
                  hasWhiteText:false
              },
              contextualStyles:[
                  { type: 'primary', hasWhiteText: true,},
                  { type: 'secondary', hasWhiteText: true,},
                  { type: 'success', hasWhiteText: true,},
                  { type: 'danger', hasWhiteText: true,},
                  { type: 'warning', hasWhiteText: true,},
                  { type: 'info', hasWhiteText: true,},
                  { type: 'light', hasWhiteText: true,},
                  { type: 'dark', hasWhiteText: true,},
              ]
          },
          
          /** progress bar*/
          progress:{
              width:50,
              backgroundcolor: '#0af'
          }
      }
  },
    computed:{
      /* hier gaan we de classes coderen voor het wijzigen van kleur in de card-header*/
        cardClasses(){
            const classes = [];
            
            if(!this.card.selectedStyling){
                return classes;
            }
            classes.push(`bg-${this.card.selectedStyling.type}`);
            
            if(this.card.selectedStyling.hasWhiteText){
                classes.push('text-white');
            }
            return classes;
            
        },
        progressStyling(){
            return{
                width: `${this.progress.width}%`,
                backgroundColor: `#${this.progress.backgroundcolor}`
            }
        }
    },
    
    filters:{
      /*eerste letter in hoofdletters*/
        ucfirst(value){
            if(!value){
                return '';
            }
            return value.charAt(0).toUpperCase() + value.slice(1);
        }
    }
 
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
