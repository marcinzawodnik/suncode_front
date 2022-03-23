<template>
<div class = "main">
    <div>
      <h2>Wybierz:</h2>
        <form action="" method="get" class="row g-3">
            <select id="select1" name="select1" class="form-select form-select-sm mb-3" aria-label=".form-select-sm example">
                <option value="Kolumna1" selected>Kolumna 1</option>
                <option value="Kolumna2">Kolumna 2</option>
                <option value="Kolumna3">Kolumna 3</option>
                <option value="Kolumna4">Kolumna 4</option>
            </select>
                <select name="select2" id="select2" class="form-select form-select-sm" aria-label=".form-select-sm example">
                <option value="Powt" selected>Powtarzalne rekordy</option>
                <option value="Niepowt">Niepowtarzalne rekordy</option>
            </select>
            <button @click="show()" type="button" value="Pokaż" class="btn btn-primary">Pokaż</button>
        </form>
    </div> 
    <div id = "bbb">
      <table id="ddd" class="table table-bordered border-secondary">
        <tr>
          <th>Id</th>
          <th>Kolumna1</th>
          <th>Kolumna2</th>
          <th>Kolumna3</th>
          <th>Kolumna4</th>
        </tr>
      </table>
    </div>   
</div>    
</template>

<script>
import axios from "axios";
export default {
    name: "dataItem",
  data() {
    return {
      data: []
    };
  },
  methods: {
    show(){
        var table = document.getElementById("ddd")
        table.innerHTML = ' <tr><th>Id</th><th>Kolumna1</th><th>Kolumna2</th>'+
          '<th>Kolumna3</th><th>Kolumna4</th></tr>';
        var selectElem1 = document.getElementById('select1');
        var column = selectElem1.selectedIndex;
        var selectElem2 = document.getElementById('select2');
        var distinct = selectElem2.selectedIndex;
        axios.get(`http://localhost:8080/data?id=`+ column + '&distinct='+distinct).then(response => {
            console.log(response.data);
            for(var i = 0; i < response.data.length; i++){                  
                table.innerHTML += '<tr><th>' + response.data[i].id +'</th>'
                + '<th>' + response.data[i].kolumna1 +'</th>'
                + '<th>' + response.data[i].kolumna2 +'</th>'
                + '<th>' + response.data[i].kolumna3 +'</th>'
                + '<th>' + response.data[i].kolumna4 +'</th></tr>';
            }
        });
      }
    },
}

</script>