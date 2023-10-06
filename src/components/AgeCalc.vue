<template>
	<div class="card">
		<div class="card_wrapper">
			<div class="age_wrapper">
				<div class="day_wrapper">
				<h4>Day</h4>
				<input name="date" placeholder="DD" v-model="days" :class="{focus: daysErrorField}" type="text">
					<h5 v-if="daysErrorField" class="error">Field is required</h5>

					<h5 v-if="daysValidation" class="error">Must be a valid day</h5>
			</div>

			<div class="month_wrapper">
				<h4>Month</h4>
				<input name="Month" placeholder="MM" v-model="month" :class="{focus: monthErrorField}">
        <h5 v-if="monthErrorField" class="error">Field is required</h5>
         <h5 v-if="monthValidation" class="error">This Month does not exist</h5>
			</div>
			<div class="year_wrapper">
				<h4>Year</h4>
				<input name="Year" placeholder="YYYY" v-model="year" :class="{focus: yearErrorField}" type="text">
				<h5 v-if="yearErrorField" class="error">Field is required</h5>
					<h5 v-if="yearValidation" class="error">Must be in the past</h5>
			</div>
			</div>
			
			<div class="arrow_wrapper">
				<div class="line"></div>
			<button @click="getAge">
				<img src="../assets/images/icon-arrow.svg">
			</button>
		</div>

		<div class="age_calculated_wrapper">
            <div class="age_years">
            	
            	<h1>
            		
            			<span>{{resultYear}}</span>
            		
            		
            			
            		
            		
            	Years
            </h1>
            </div>
             <div class="age_months">
             	<h1>
             			<span>{{resultMonth}}</span>
            		
             	
            	Months
             	</h1>
            	
            </div>
             <div class="age_days">
             	<h1>
             			<span>{{resultDay}}</span>
            	Days
             	</h1>
            	
            </div>
			</div>

		</div>	
	</div>
</template>

<script>
export default {

  name: 'AgeCalc',

  data () {
    return {
       year: "",
       month: '',
       days: '',
       resultYear: '--',
       resultMonth: '--',
       resultDay:'--',

       yearErrorField: false,
       monthErrorField: false,
       daysErrorField: false,
       yearValidation: false,
       monthValidation: false,
       daysValidation: false
    }
  },
  methods: {
  	getAge(){
  		const date = new Date()
      
      if (this.year.length === 0){
      	this.yearErrorField = true
      	 
       } 
       else if(this.year > date.getFullYear()){
         this.yearValidation = true
         
      } 

      else {
      	this.yearErrorField = false
      	this.yearValidation = false
      }

      if (this.month.length === 0){
      	
      	 this.monthErrorField = true
      	
      } else if (this.month < 1 || this.month > 12){
this.monthValidation = true
      }
      else {
      	this.monthErrorField = false
      }

      if (this.days.length === 0){
      	
      	this.daysErrorField = true
      }else if (this.days < 1 || this.days > 31){
          this.daysValidation = true
      } 
      else {
      	this.daysErrorField = false
      }

     if(this.days === "" && this.month === "" && this.year === ""){
     	  this.resultDay = "--"
     	  this.resultMonth = "--"
     	  this.resultYear = "--"
     } else if(this.days === "" || this.month === "" || this.year === ""){
this.resultDay = "--"
     	  this.resultMonth = "--"
     	  this.resultYear = "--"
     } else if (this.year > date.getFullYear()){
     	this.resultDay = "--"
     	  this.resultMonth = "--"
     	  this.resultYear = "--"

     }

     else {
     	 this.resultDay = date.getDate() < this.days ? this.days - date.getDate(): date.getDate() - this.days
            this.resultMonth = date.getMonth() - this.month
            this.resultYear = date.getFullYear() - this.year        
            return 

     }
       	
  	}
  }
}
</script>

<style src="./AgeCalc.css"></style>