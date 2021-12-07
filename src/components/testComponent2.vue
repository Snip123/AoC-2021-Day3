<template>
  <div class="counter">
    <textarea v-model="message" placeholder="add multiple lines"></textarea>
    <br />
    <button @click="updateData">Update</button>
    <br/>
    <span>Output:</span>
    <p style="white-space: pre-line;">{{ output }}</p>
    
  </div>
</template>

<script>

export default {
  name: 'testComponent2',
  data: function() {
    return {
      message: "",
      output: ""
    }
  },
  methods:
  {
    updateData: function () {


      
      /*var test_inputs = [
"00100",
"11110",
"10110",
"10111",
"10101",
"01111",
"00111",
"11100",
"10000",
"11001",
"00010",
"01010"
];
     var inputlines = test_inputs;*/
     var inputlines = this.message.split('\n');
      
      var PowerDiagnosticsCount = inputlines.reduce(reduceAoCLine);
      var halfLength = inputlines.length/2
      var gammaesp = calcGammaESP(PowerDiagnosticsCount,halfLength)
      var O2 = calcO2(PowerDiagnosticsCount, inputlines)
      var CO2 = calcCO2(PowerDiagnosticsCount, inputlines)
      console.log(O2);
      console.log(CO2)
      this.output = "life support " + (O2*CO2) + "\n"
      this.output += "total " + (gammaesp.gamma*gammaesp.esp) + "gamma " + gammaesp.gamma + " esp " +gammaesp.esp + " " + PowerDiagnosticsCount
    }
  }
}
function calcGammaESP(PowerDiagnosticsCount,halfLength)
{
  var gamma = "";
      for (let index = 0; index < PowerDiagnosticsCount.length; index++) {
        const element = PowerDiagnosticsCount[index];
        if(element > halfLength)
        {
          gamma += "1"
        }
        else
        {
          gamma += "0"
        }
      }
      console.log("test")
      // eslint-disable-next-line no-undef
      var gammanumber = BigInt(0);
      // eslint-disable-next-line no-undef
      var espnumber = BigInt(0);
      for (let index = length; index < gamma.length; index++) {
        const element = gamma[index];
        if(element ==="1")
        {
          // eslint-disable-next-line no-undef
          gammanumber+= BigInt(Math.pow(2,gamma.length-index-1))
        }
        else{
            // eslint-disable-next-line no-undef
            espnumber+= BigInt(Math.pow(2,gamma.length-index-1))

        }
      }
      return { gamma: gammanumber, esp:espnumber}
}

function  calcO2 (PowerDiagnosticsCount,inputlines)
{
  var currentCount = PowerDiagnosticsCount;
  for (let index = 0; index < PowerDiagnosticsCount.length; index++) {
    const element = currentCount[index];
    console.log("calcing o2 "+inputlines.length + " index " + index)
        console.log(inputlines)
    console.log(currentCount)
    if(element>=inputlines.length/2)
    {
    inputlines = inputlines.filter(line => line[index] === '1')
    currentCount = inputlines.reduce(reduceAoCLine)
    console.log("pass calcing o2 "+inputlines.length + " index " + index)

    }
    else
    {
        inputlines = inputlines.filter(line => line[index] === '0')
    currentCount = inputlines.reduce(reduceAoCLine)
    console.log("fail calcing o2 "+inputlines.length + " index " + index)
  
    }
    
    
    if(inputlines.length ===1)
      break;
  }
      // eslint-disable-next-line no-undef
      var O2 = (0);
      for (let index = length; index < inputlines[0].length; index++) {
        const element = inputlines[0][index];
        if(element ==="1")
        {
          // eslint-disable-next-line no-undef
          O2+= (Math.pow(2,inputlines[0].length-index-1))
        }
      }
  return O2
}
function  calcCO2 (PowerDiagnosticsCount,inputlines)
{
  var currentCount = PowerDiagnosticsCount;
  for (let index = 0; index < PowerDiagnosticsCount.length; index++) {
    const element = currentCount[index];
    console.log("calcing co2 "+inputlines.length + " index " + index)
        console.log(inputlines)
    console.log(currentCount)
    if(element<inputlines.length/2)
    {
    inputlines = inputlines.filter(line => line[index] === '1')
    currentCount = inputlines.reduce(reduceAoCLine)
    console.log("pass calcing co2 "+inputlines.length + " index " + index)

    }
    else
    {
        inputlines = inputlines.filter(line => line[index] === '0')
    currentCount = inputlines.reduce(reduceAoCLine)
    console.log("fail calcing co2 "+inputlines.length + " index " + index)
  
    }
    
    
    if(inputlines.length ===1)
      break;
  }
      // eslint-disable-next-line no-undef
      var CO2 = (0);
      for (let index = length; index < inputlines[0].length; index++) {
        const element = inputlines[0][index];
        if(element ==="1")
        {
          // eslint-disable-next-line no-undef
          CO2+= (Math.pow(2,inputlines[0].length-index-1))
        }
      }
  return CO2
}

function mapAoCLine(line)
{
  return line.split('');
}

function reduceAoCLine(total, line)
{
  if(total ===null)
    return mapAoCLine(line);
  var component = mapAoCLine(line);
var newtotal= new Array();
  for (let index = 0; index < component.length; index++) {
    var element = parseInt(component[index]);
    var totalInt = parseInt(total[index])
    newtotal[index] = element+ totalInt; 
  }
  return newtotal;
}
</script>

