<template>
	<div ref="container" id="DropAndList">
		<vue-dropzone
		v-if="jsonNeeded"
		ref="dropzone"
		id="drop1"
		:options="dropOptions"
		@vdropzone-success="atUploadSuccess"
		></vue-dropzone>
		<tree-view v-else :data="json" :options="{maxDepth: 3}"></tree-view>
	</div>
</template>

<script>
import 'vue2-dropzone/dist/vue2Dropzone.min.css';
import vueDropzone from "vue2-dropzone";
import Papa from 'papaparse'



export default {
  data: () => ({
    dropOptions: {
		url: 'https://httpbin.org/post',
		acceptedFiles: ".CSV,.csv",
		addRemoveLinks: true,
		maxFiles: 1
	},
	json: {
		
	},
	jsonNeeded: true
  }),
  components: {
    vueDropzone
  },
  methods: {
	atUploadSuccess(file) {
		this.changeToList(file);
	},

	changeToList(file) {
		var self = this;

		Papa.parse(file, {
			complete: function(results) {
				var list_of_rows = results.data;
				list_of_rows.splice(0,1);
				list_of_rows.splice(list_of_rows.length-1,1);
				var serieList = {};
				console.log(list_of_rows[list_of_rows.length-1]);
				for(var row of list_of_rows) {
					serieList['Total_De_Conteúdo_Assistido'] += 1
					var indexOfSeason = "";
					var rowTitle = "";
					var rowEpisode = "";
					var rowSeason = "";
					var indexOfEpisode = "";
					
					if(row[0].indexOf(": Temporada") !== -1) {
						indexOfSeason = row[0].indexOf(": Temporada");
						indexOfEpisode = indexOfSeason + 15;
						rowSeason = row[0].slice(indexOfSeason+2, row[0].indexOf(':',indexOfSeason+2)).trim();
						rowEpisode = row[0].slice(indexOfEpisode,row[0].length).trim();
						rowTitle = row[0].slice(0,indexOfSeason).trim().replace("/ /gi", "_");

						console.log(indexOfSeason, indexOfEpisode, rowSeason, rowEpisode, rowTitle)
					} else if(row[0].indexOf(": Limited Série") !== -1) {
						indexOfSeason = row[0].indexOf(": Limited Série")
						indexOfEpisode = indexOfSeason + 17;
						rowSeason = row[0].slice(indexOfSeason+2, row[0].indexOf(':',indexOfSeason+2)).trim();
						rowEpisode = row[0].slice(indexOfEpisode,row[0].length).trim();
						rowTitle = row[0].slice(0,indexOfSeason).trim().replace("/ /gi", "_");

						console.log(indexOfSeason, indexOfEpisode, rowSeason, rowEpisode, rowTitle)
					} else {
						rowTitle = row[0].trim().replace("/ /gi", "_");
						console.log(rowTitle);
					}

					var rowDate = row[1];
					// var rowDay = rowDate.slice(0,2);
					// var rowMonth = rowDate.slice(3,5);
					// var rowYear = rowDate.slice(rowDate.length-4,rowDate.length);

					if(rowTitle in serieList) {
						serieList[rowTitle]['Episodios_Assistidos'] += 1
						if(rowSeason in serieList[rowTitle] && rowDate in serieList[rowTitle][rowSeason]) {
							serieList[rowTitle][rowSeason][rowDate].unshift(rowEpisode)
						} else if(!(rowSeason in serieList[rowTitle])) {
							serieList[rowTitle][rowSeason] = {[rowDate]: [rowEpisode]}
						} else {
							serieList[rowTitle][rowSeason][rowDate] = [rowEpisode]
						}
					} else {
						serieList[rowTitle] = {'Episodios_Assistidos': 1}
						serieList[rowTitle][rowSeason] = {[rowDate]: [rowEpisode]}
					}
				}

				self.json = serieList;
				self.jsonNeeded = false;
				console.log(self);
			}
		});
	}
  }
};
</script>


<style scoped>
	@import 'https://fonts.googleapis.com/icon?family=Material+Icons';

	#DropAndList {
		padding: 50px;
	}
</style>
