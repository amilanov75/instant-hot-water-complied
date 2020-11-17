<!-- html section -->
<template lang="html">
   <!-- This is where the output from the Vue #app is displayed -->
    <b-container style="color: #c2c2c2;" >
        <div>
            <template id = "hot water timer" >

                <!-- ****************** RELOAD PAGE BUTTON ****************** -->
                <div style="position:absolute; width:150px;  left:1760px; top:72px;" > <button style="color:grey; font-size:80% !important;" v-on:click="reloadPage()"> Reload Page </button></div> 

                <!-- ****************** TEMPS / PUMP STATUS ****************** -->
                <div class="input-card" style="position:absolute; width:500px; left:-65px; top:118px;"> 

                    <div style="position:absolute; width:100px; left:1428px; top:-26px; color:grey; font-size:var(--font-size-medium)"> Current </div>
                    <div style="position:absolute; width:100px; left:1506px; top:-26px; color:grey; font-size:var(--font-size-medium)"> T-1 </div>
                    <div style="position:absolute; width:100px; left:1568px; top:-26px; color:grey; font-size:var(--font-size-medium)"> T-2 </div>
                    <div style="position:absolute; width:100px; left:1634px; top:-26px; color:grey; font-size:var(--font-size-medium)"> T-3 </div>

                    <!-- ************************************************* PUMP IMAGES / WATER FLOWING ANIMATION ********************************************** -->
                    <!-- ************************************************************************************************************************************** -->
                    <!-- ************************************************************** KITCHEN *************************************************************** -->
                    <!-- ************************************************************************************************************************************** -->
                    <div class="input-card" style="position:absolute; left:-160px; top:0px;"> 
                        <!-- ************************************************************** LHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:400px; height:58px; left:1120px; top:0px; font-size:var(--font-size-medium);" :style="{backgroundColor: hw_values[0].pump_schedule?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <!-- WATER PIPES FROM RHS -->
                            <div style="position:absolute; width:95px;  left:755px;  top:10px; font-size:var(--font-size-medium);" :style="{color: hw_values[0].pump_status? '': 'var(--colour-temp-rhs-pipes)'}"> <p> {{hw_values[1].actual}} C </p></div>
                            <div style="position:absolute; width:120px; left:720px;  top:33px;">                       <b-progress :value="100" height="7" :variant="hw_values[0].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[0].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:7px;   left:833px;  top:34px;" class="RotatePipe180"> <b-progress :value="100" height="93":variant="hw_values[0].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[0].pump_status"></b-progress> </div>
                            <!-- WATER PIPES FROM LHS -->
                            <div style="position:absolute; width:360px; left:-181px; top:-12px; color:grey; font-size:var(--font-size-medium);"> {{hw_values[0].pump_status? 'Return':''}} </div>
                            <div style="position:absolute; width:7px;   left:-233px; top:12px;"> <b-progress :value="100" height="90" :variant="hw_values[0].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[0].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:120px; left:-233px; top:12px;"> <b-progress :value="100" height="7"  :variant="hw_values[0].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[0].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:35px;  left:-35px;  top:35px;"> <b-progress :value="100" height="7"  :variant="hw_values[0].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[0].pump_status"></b-progress> </div>
                            <!-- PUMP IMAGES -->
                            <div v-if="hw_values[0].pump_status"> <figure style="position:absolute; width:90px;  left:-120px; top:0px;"> <img style = "max-width:95%;" src="../../src/images/pump_on_return.gif">  </img> </figure> </div>
                            <div v-else>                          <figure style="position:absolute; width:90px;  left:-120px; top:0px;"> <img style = "max-width:95%;" src="../../src/images/pump_off_return.png"> </img> </figure> </div>
                            <!-- MAIN CARD -->
                            <div style="position:absolute; width:250px; left:20px;  top:7px;font-size:var(--font-size-large)"><p > Kitchen </p>    </div> 
                            <div style="position:absolute; width:250px; left:100px; top:7px;" >                               <p > A {{hw_values[1].actual}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:7px;  color:grey; font-size:var(--font-size-medium);" >   <p > {{varianceTarget(1)}} C     </p></div>
                            <div style="position:absolute; width:250px; left:100px; top:32px; color:grey;" >                  <p > T {{hw_values[1].target}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:32px; color:grey; font-size:var(--font-size-medium);" >   <p > D {{hw_values[1].target + hw_values[11].delta_C}} C </p></div>
                    <!-- BAR CHARTS -->
                    <b-progress style="position:absolute; width:150px; left:170px; top:12px; backgroundColor:transparent;       border-radius:0px;"                             :value="tempProgressBar(hw_values[1].actual)"   height="9"  :variant="hw_values[0].pump_status? 'hw-pipe-red':'hw-pipe-blue'"> </b-progress> 
                    <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;       border-radius:0px;"                             :value="tempProgressBar(hw_values[1].target + hw_values[11].delta_C)" height="9"  :variant="hw_values[0].pump_status? 'hw-pipe-red':'hw-pipe-blue'"></b-progress> 
                    <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;       border-radius:0px;"  class="target-process"     :value="tempProgressBar(hw_values[1].target)"   height="9"  :variant="hw_values[0].pump_status? 'hw-pipe-grey':'hw-pipe-grey'"></b-progress> 
                        </div>
                        <!-- ************************************************************** RHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:310px; height:58px; left:1530px; top:0px;" :style="{backgroundColor: hw_values[0].pump_schedule?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <div style="position:absolute; width:30px;  left:15px; top:7px;  color:grey; font-size:var(--font-size-medium);" >   <p > On </p></div>
                            <div style="position:absolute; width:30px;  left:15px; top:32px; color:grey; font-size:var(--font-size-medium);" >   <p > Off </p></div>
                            <!-- TIMERS -->
                            <div style="position:absolute; width:30px;  left:65px; top:7px;   color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[0].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[0].run_time.time1 > 43200? '>12hrs': hw_values[0].run_time.time1 < 3600? new Date(hw_values[0].run_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[0].run_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:65px; top:32px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[0].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[0].off_time.time1 > 43200? '>12hrs': hw_values[0].off_time.time1 < 3600? new Date(hw_values[0].off_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[0].off_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[0].run_time.time2 > 43200? '>12hrs': hw_values[0].run_time.time2 < 3600? new Date(hw_values[0].run_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[0].run_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[0].off_time.time2 > 43200? '>12hrs': hw_values[0].off_time.time2 < 3600? new Date(hw_values[0].off_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[0].off_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[0].run_time.time3 > 43200? '>12hrs': hw_values[0].run_time.time3 < 3600? new Date(hw_values[0].run_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[0].run_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[0].off_time.time3 > 43200? '>12hrs': hw_values[0].off_time.time3 < 3600? new Date(hw_values[0].off_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[0].off_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[0].run_time.time4 > 43200? '>12hrs': hw_values[0].run_time.time4 < 3600? new Date(hw_values[0].run_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[0].run_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[0].off_time.time4 > 43200? '>12hrs': hw_values[0].off_time.time4 < 3600? new Date(hw_values[0].off_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[0].off_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                        </div> 
                    </div>


                    <!-- ************************************************************************************************************************************** -->
                    <!-- ************************************************************** MASTER *************************************************************** -->
                    <!-- ************************************************************************************************************************************** -->
                    <div class="input-card" style="position:absolute; left:-160px; top:0px;"> 
                        <!-- ************************************************************** LHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:400px; height:58px; left:1120px; top:80px; font-size:var(--font-size-medium);" :style="{backgroundColor: hw_values[2].pump_schedule?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <!-- WATER PIPES FROM RHS -->
                            <div style="position:absolute; width:95px; left:755px;  top:10px; font-size:var(--font-size-medium);"  :style="{color: hw_values[2].pump_status? '': 'var(--colour-temp-rhs-pipes)' }"> <p> {{hw_values[3].actual}} C </p></div>
                            <div style="position:absolute; width:120px; left:720px;  top:33px;">                       <b-progress :value="100" height="7" :variant="hw_values[2].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[2].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:7px;   left:833px;  top:32px;" class="RotatePipe180"> <b-progress :value="100" height="93"
                                :variant="(hw_values[0].pump_status || hw_values[2].pump_status)? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="(hw_values[0].pump_status || hw_values[2].pump_status)"></b-progress> </div>
                            <!-- WATER PIPES FROM LHS -->
                            <div style="position:absolute; width:360px; left:-181px; top:-12px; color:grey; font-size:var(--font-size-medium);"> {{hw_values[2].pump_status? 'Return':''}} </div>
                            <div style="position:absolute; width:7px;   left:-233px; top:12px;"> <b-progress :value="100" height="90" :variant="hw_values[2].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[2].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:120px; left:-233px; top:12px;"> <b-progress :value="100" height="7"  :variant="hw_values[2].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[2].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:35px;  left:-35px;  top:35px;"> <b-progress :value="100" height="7"  :variant="hw_values[2].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[2].pump_status"></b-progress> </div>
                            <!-- PUMP IMAGES -->
                            <div v-if="hw_values[2].pump_status"> <figure style="position:absolute; width:90px;  left:-120px; top:0px;"> <img style = "max-width:95%;" src="../../src/images/pump_on_return.gif">  </img> </figure> </div>
                            <div v-else>                          <figure style="position:absolute; width:90px;  left:-120px; top:0px;"> <img style = "max-width:95%;" src="../../src/images/pump_off_return.png"> </img> </figure> </div>
                            <!-- MAIN CARD -->
                            <div style="position:absolute; width:250px; left:20px;  top:7px;font-size:var(--font-size-large)"><p > Master </p>    </div> 
                            <div style="position:absolute; width:250px; left:100px; top:7px;" >                               <p > A {{hw_values[3].actual}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:7px;  color:grey; font-size:var(--font-size-medium);" >   <p > {{varianceTarget(1)}} C     </p></div>
                            <div style="position:absolute; width:250px; left:100px; top:32px; color:grey;" >                  <p > T {{hw_values[3].target}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:32px; color:grey; font-size:var(--font-size-medium);" >   <p > D {{hw_values[3].target + hw_values[11].delta_C}} C </p></div>
                    <!-- BAR CHARTS -->
                    <b-progress style="position:absolute; width:150px; left:170px; top:12px; backgroundColor:transparent;   border-radius:0px;"                             :value="tempProgressBar(hw_values[3].actual)"   height="9"  :variant="hw_values[2].pump_status? 'hw-pipe-red':'hw-pipe-blue'"> </b-progress> 
                    <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;   border-radius:0px;"                             :value="tempProgressBar(hw_values[3].target + hw_values[11].delta_C)" height="9"  :variant="hw_values[2].pump_status? 'hw-pipe-red':'hw-pipe-blue'"></b-progress> 
                    <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;   border-radius:0px;"  class="target-process"     :value="tempProgressBar(hw_values[3].target)"   height="9"  :variant="hw_values[2].pump_status? 'hw-pipe-grey':'hw-pipe-grey'"></b-progress> 
                        </div>
                        <!-- ************************************************************** RHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:310px; height:58px; left:1530px; top:80px;" :style="{backgroundColor: hw_values[2].pump_schedule?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <div style="position:absolute; width:30px;  left:15px; top:7px;  color:grey; font-size:var(--font-size-medium);" >   <p > On </p></div>
                            <div style="position:absolute; width:30px;  left:15px; top:32px; color:grey; font-size:var(--font-size-medium);" >   <p > Off </p></div>
                            <!-- TIMERS -->
                            <div style="position:absolute; width:30px;  left:65px; top:7px;   color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[2].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[2].run_time.time1 > 43200? '>12hrs': hw_values[2].run_time.time1 < 3600? new Date(hw_values[2].run_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[2].run_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:65px; top:32px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[2].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[2].off_time.time1 > 43200? '>12hrs': hw_values[2].off_time.time1 < 3600? new Date(hw_values[2].off_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[2].off_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[2].run_time.time2 > 43200? '>12hrs': hw_values[2].run_time.time2 < 3600? new Date(hw_values[2].run_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[2].run_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[2].off_time.time2 > 43200? '>12hrs': hw_values[2].off_time.time2 < 3600? new Date(hw_values[2].off_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[2].off_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[2].run_time.time3 > 43200? '>12hrs': hw_values[2].run_time.time3 < 3600? new Date(hw_values[2].run_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[2].run_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[2].off_time.time3 > 43200? '>12hrs': hw_values[2].off_time.time3 < 3600? new Date(hw_values[2].off_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[2].off_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[2].run_time.time4 > 43200? '>12hrs': hw_values[2].run_time.time4 < 3600? new Date(hw_values[2].run_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[2].run_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[2].off_time.time4 > 43200? '>12hrs': hw_values[2].off_time.time4 < 3600? new Date(hw_values[2].off_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[2].off_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                        </div> 
                    </div>



                    <!-- ************************************************************************************************************************************** -->
                    <!-- ************************************************************** 1ST LOFT ************************************************************** -->
                    <!-- ************************************************************************************************************************************** -->
                    <div class="input-card" style="position:absolute; left:-160px; top:0px;"> 
                        <!-- ************************************************************** LHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:400px; height:58px; left:1120px; top:160px; font-size:var(--font-size-medium);" :style="{backgroundColor: hw_values[4].pump_schedule?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <!-- WATER PIPES FROM RHS -->
                            <div style="position:absolute; width:95px; left:755px;  top:10px; font-size:var(--font-size-medium);"  :style="{color: hw_values[5].pump_status? '': 'var(--colour-temp-rhs-pipes)' }"> <p> {{hw_values[5].actual}} C </p></div>
                            <div style="position:absolute; width:120px; left:720px;  top:33px;">                       <b-progress :value="100" height="7" :variant="hw_values[4].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[4].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:7px;   left:833px;  top:32px;" class="RotatePipe180"> <b-progress :value="100" height="93"
                                :variant="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status)? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status)"></b-progress> </div>
                            <!-- WATER PIPES FROM LHS -->
                            <div style="position:absolute; width:360px; left:-181px; top:-12px; color:grey; font-size:var(--font-size-medium);"> {{hw_values[4].pump_status? 'Return':''}} </div>
                            <div style="position:absolute; width:120px; left:-233px; top:12px;"> <b-progress :value="100" height="7"  :variant="hw_values[4].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[4].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:35px;  left:-35px;  top:35px;"> <b-progress :value="100" height="7"  :variant="hw_values[4].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[4].pump_status"></b-progress> </div>
                            <!-- PUMP IMAGES -->
                            <div v-if="hw_values[4].pump_status"> <figure style="position:absolute; width:90px;  left:-120px; top:0px;"> <img style = "max-width:95%;" src="../../src/images/pump_on_return.gif">  </img> </figure> </div>
                            <div v-else>                          <figure style="position:absolute; width:90px;  left:-120px; top:0px;"> <img style = "max-width:95%;" src="../../src/images/pump_off_return.png"> </img> </figure> </div>
                            <!-- MAIN CARD -->
                            <div style="position:absolute; width:250px; left:20px;  top:7px;font-size:var(--font-size-large)"><p > 1st Loft </p>    </div> 
                            <div style="position:absolute; width:250px; left:100px; top:7px;" >                               <p > A {{hw_values[5].actual}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:7px;  color:grey; font-size:var(--font-size-medium);" >   <p > {{varianceTarget(1)}} C     </p></div>
                            <div style="position:absolute; width:250px; left:100px; top:32px; color:grey;" >                  <p > T {{hw_values[5].target}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:32px; color:grey; font-size:var(--font-size-medium);" >   <p > D {{hw_values[5].target + hw_values[11].delta_C}} C </p></div>
                    <!-- BAR CHARTS -->
                    <b-progress style="position:absolute; width:150px; left:170px; top:12px; backgroundColor:transparent;       border-radius:0px;"                             :value="tempProgressBar(hw_values[5].actual)"   height="9"  :variant="hw_values[4].pump_status? 'hw-pipe-red':'hw-pipe-blue'"> </b-progress> 
                    <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;       border-radius:0px;"                             :value="tempProgressBar(hw_values[5].target + hw_values[11].delta_C)" height="9"  :variant="hw_values[4].pump_status? 'hw-pipe-red':'hw-pipe-blue'"></b-progress> 
                    <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;       border-radius:0px;"  class="target-process"     :value="tempProgressBar(hw_values[5].target)"   height="9"  :variant="hw_values[4].pump_status? 'hw-pipe-grey':'hw-pipe-grey'"></b-progress> 
                        </div>
                        <!-- ************************************************************** RHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:310px; height:58px; left:1530px; top:160px;" :style="{backgroundColor: hw_values[4].pump_schedule?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <div style="position:absolute; width:30px;  left:15px; top:7px;  color:grey; font-size:var(--font-size-medium);" >   <p > On </p></div>
                            <div style="position:absolute; width:30px;  left:15px; top:32px; color:grey; font-size:var(--font-size-medium);" >   <p > Off </p></div>
                            <!-- TIMERS -->
                            <div style="position:absolute; width:30px;  left:65px; top:7px;   color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[4].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[4].run_time.time1 > 43200? '>12hrs': hw_values[4].run_time.time1 < 3600? new Date(hw_values[4].run_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[4].run_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:65px; top:32px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[4].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[4].off_time.time1 > 43200? '>12hrs': hw_values[4].off_time.time1 < 3600? new Date(hw_values[4].off_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[4].off_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[4].run_time.time2 > 43200? '>12hrs': hw_values[4].run_time.time2 < 3600? new Date(hw_values[4].run_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[4].run_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[4].off_time.time2 > 43200? '>12hrs': hw_values[4].off_time.time2 < 3600? new Date(hw_values[4].off_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[4].off_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[4].run_time.time3 > 43200? '>12hrs': hw_values[4].run_time.time3 < 3600? new Date(hw_values[4].run_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[4].run_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[4].off_time.time3 > 43200? '>12hrs': hw_values[4].off_time.time3 < 3600? new Date(hw_values[4].off_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[4].off_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[4].run_time.time4 > 43200? '>12hrs': hw_values[4].run_time.time4 < 3600? new Date(hw_values[4].run_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[4].run_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[4].off_time.time4 > 43200? '>12hrs': hw_values[4].off_time.time4 < 3600? new Date(hw_values[4].off_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[4].off_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                        </div> 
                    </div>




                    <!-- ************************************************************************************************************************************** -->
                    <!-- ************************************************************** GARDEN **************************************************************** -->
                    <!-- ************************************************************************************************************************************** -->
                    <div class="input-card" style="position:absolute; left:-160px; top:0px;"> 
                        <!-- ************************************************************** LHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:400px; height:58px; left:1120px; top:240px; font-size:var(--font-size-medium);" :style="{backgroundColor: hw_values[6].pump_schedule?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <!-- WATER PIPES FROM RHS -->
                            <div style="position:absolute; width:95px; left:755px;  top:10px; font-size:var(--font-size-medium);"  :style="{color: hw_values[6].pump_status? '': 'var(--colour-temp-rhs-pipes)' }"> <p> {{hw_values[7].actual}} C </p></div>
                            <div style="position:absolute; width:120px; left:720px;  top:33px;">                       <b-progress :value="100" height="7"  :variant="hw_values[6].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[6].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:7px;   left:833px;  top:32px;" class="RotatePipe180"> <b-progress :value="100" height="115"
                                :variant="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status)? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status)"></b-progress> </div>
                            <!-- WATER PIPES FROM LHS -->
                            <div style="position:absolute; width:360px; left:-181px; top:-12px; color:grey; font-size:var(--font-size-medium);"> {{hw_values[6].pump_status? 'Return':''}} </div>
                            <div style="position:absolute; width:7px;   left:-233px; top:-70px;"class="RotatePipe180"> <b-progress :value="100" height="86" :variant="hw_values[6].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[6].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:120px; left:-233px; top:12px;"> <b-progress :value="100" height="7"  :variant="hw_values[6].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[6].pump_status"></b-progress> </div>
                            <div style="position:absolute; width:35px;  left:-35px;  top:35px;"> <b-progress :value="100" height="7"  :variant="hw_values[6].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[6].pump_status"></b-progress> </div>
                            <!-- PUMP IMAGES -->
                            <div v-if="hw_values[6].pump_status"> <figure style="position:absolute; width:90px;  left:-120px; top:0px;"> <img style = "max-width:95%;" src="../../src/images/pump_on_return.gif">  </img> </figure> </div>
                            <div v-else>                          <figure style="position:absolute; width:90px;  left:-120px; top:0px;"> <img style = "max-width:95%;" src="../../src/images/pump_off_return.png"> </img> </figure> </div>
                            <!-- MAIN CARD -->
                            <div style="position:absolute; width:250px; left:20px;  top:7px;font-size:var(--font-size-large)"><p > Garden </p>    </div> 
                            <div style="position:absolute; width:250px; left:100px; top:7px;" >                               <p > A {{hw_values[7].actual}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:7px;  color:grey; font-size:var(--font-size-medium);" >   <p > {{varianceTarget(1)}} C     </p></div>
                            <div style="position:absolute; width:250px; left:100px; top:32px; color:grey;" >                  <p > T {{hw_values[7].target}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:32px; color:grey; font-size:var(--font-size-medium);" >   <p > D {{hw_values[7].target + hw_values[11].delta_C}} C </p></div>
                    <!-- BAR CHARTS -->
                    <b-progress style="position:absolute; width:150px; left:170px; top:12px; backgroundColor:transparent;   border-radius:0px;"                             :value="tempProgressBar(hw_values[7].actual)"   height="9"  :variant="hw_values[6].pump_status? 'hw-pipe-red':'hw-pipe-blue'"> </b-progress> 
                    <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;   border-radius:0px;"                             :value="tempProgressBar(hw_values[7].target + hw_values[11].delta_C)" height="9"  :variant="hw_values[6].pump_status? 'hw-pipe-red':'hw-pipe-blue'"></b-progress> 
                    <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;   border-radius:0px;"  class="target-process"     :value="tempProgressBar(hw_values[7].target)"   height="9"  :variant="hw_values[6].pump_status? 'hw-pipe-grey':'hw-pipe-grey'"></b-progress> 
                        </div>
                        <!-- ************************************************************** RHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:310px; height:58px; left:1530px; top:240px;" :style="{backgroundColor: hw_values[6].pump_schedule?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <div style="position:absolute; width:30px;  left:15px; top:7px;  color:grey; font-size:var(--font-size-medium);" >   <p > On </p></div>
                            <div style="position:absolute; width:30px;  left:15px; top:32px; color:grey; font-size:var(--font-size-medium);" >   <p > Off </p></div>
                            <!-- TIMERS -->
                            <div style="position:absolute; width:30px;  left:65px; top:7px;   color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[6].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[6].run_time.time1 > 43200? '>12hrs': hw_values[6].run_time.time1 < 3600? new Date(hw_values[6].run_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[6].run_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:65px; top:32px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[6].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[6].off_time.time1 > 43200? '>12hrs': hw_values[6].off_time.time1 < 3600? new Date(hw_values[6].off_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[6].off_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[6].run_time.time2 > 43200? '>12hrs': hw_values[6].run_time.time2 < 3600? new Date(hw_values[6].run_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[6].run_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[6].off_time.time2 > 43200? '>12hrs': hw_values[6].off_time.time2 < 3600? new Date(hw_values[6].off_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[6].off_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[6].run_time.time3 > 43200? '>12hrs': hw_values[6].run_time.time3 < 3600? new Date(hw_values[6].run_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[6].run_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[6].off_time.time3 > 43200? '>12hrs': hw_values[6].off_time.time3 < 3600? new Date(hw_values[6].off_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[6].off_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[6].run_time.time4 > 43200? '>12hrs': hw_values[6].run_time.time4 < 3600? new Date(hw_values[6].run_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[6].run_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[6].off_time.time4 > 43200? '>12hrs': hw_values[6].off_time.time4 < 3600? new Date(hw_values[6].off_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[6].off_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                        </div> 
                    </div>



                    <!-- ************************************************************************************************************************************** -->
                    <!-- ************************************************************** CYLINDER ************************************************************** -->
                    <!-- ************************************************************************************************************************************** -->
                    <!-- *** CYLINER SUPPLY *************************** -->
                    <div class="input-card" style="position:absolute; left:-160px; top:0px;"> 
                        <!-- ************************************************************** LHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:400px; height:58px; left:1120px; top:350px; font-size:var(--font-size-medium);" :style="{backgroundColor: hw_values[8].pump_status?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <!-- WATER PIPES FROM RHS -->
                            <div style="position:absolute; width:100px; left:755px;  top:10px; font-size:var(--font-size-medium);"  :style="{color: hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status? '': 'var(--colour-temp-rhs-pipes)'}"> <p> {{hw_values[9].actual}} C </p></div>
                            <div style="position:absolute; width:120px; left:720px; top:36px;"   class="RotatePipe180" > <b-progress :value="100" height="7"   
                                :variant="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status)? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status)"></b-progress> </div>
                            <!-- WATER PIPES FROM LHS -->
                            <div style="position:absolute; width:362px; left:-210px; top:10px; color:grey; font-size:var(--font-size-medium);"> {{(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status)? 'Cylinder Supply':''}} </div>
                            <div style="position:absolute; width:7px;  left:-393px; top:-189px;" >                        <b-progress :value="100" height="227"  :variant="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status)? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status)"></b-progress> </div>
                            <div style="position:absolute; width:392px; left:-393px; top:33px;"   class="RotatePipe180" > <b-progress :value="100" height="7"    :variant="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status)? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="(hw_values[0].pump_status || hw_values[2].pump_status || hw_values[4].pump_status || hw_values[6].pump_status)"></b-progress> </div>
                            <div style="position:absolute; width:250px; left:20px;  top:7px;font-size:var(--font-size-large)"><p > Cylinder </p>    </div> 
                            <div style="position:absolute; width:250px; left:100px; top:7px;" >                               <p > A {{hw_values[9].actual}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:7px;  color:grey; font-size:var(--font-size-medium);" >   <p > {{varianceTarget(9)}} C     </p></div>
                            <div style="position:absolute; width:250px; left:100px; top:32px; color:grey;" >                  <p > T {{hw_values[9].target}} C   </p></div>
                            <div style="position:absolute; width:250px; left:335px; top:32px; color:grey; font-size:var(--font-size-medium);" >   <p > D {{hw_values[9].target + hw_values[11].delta_C}} C </p></div>
                     <!-- BAR CHARTS -->
                     <b-progress style="position:absolute; width:150px; left:170px; top:12px; backgroundColor:transparent;      border-radius:0px;"                             :value="tempProgressBar(hw_values[9].actual)"   height="9"  :variant="hw_values[8].pump_status? 'hw-pipe-red':'hw-pipe-blue'"></b-progress> 
                     <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;      border-radius:0px;"                             :value="tempProgressBar(hw_values[9].target + hw_values[11].delta_C)" height="9"  :variant="hw_values[8].pump_status? 'red':'blue'"></b-progress> 
                     <b-progress style="position:absolute; width:150px; left:170px; top:37px; backgroundColor:transparent;      border-radius:0px;"  class="target-process"     :value="tempProgressBar(hw_values[9].target)"   height="9"  :variant="hw_values[8].pump_status? 'hw-pipe-grey':'hw-pipe-grey'"></b-progress> 
                        </div>
                        <!-- ************************************************************** RHS CARD ************************************************************** -->
                        <div class="card" style="position:absolute; width:310px; height:58px; left:1530px; top:350px;" :style="{backgroundColor: hw_values[8].pump_status?'var(--background-colour-pump_true)':'var(--background-colour-pump_false)'}">
                            <div style="position:absolute; width:30px;  left:15px; top:7px;   color:grey; font-size:var(--font-size-medium);" >   <p > On </p></div>
                            <div style="position:absolute; width:30px;  left:15px; top:32px;  color:grey; font-size:var(--font-size-medium);" >   <p > Off </p></div>
                            <!-- TIMERS -->
                            <div style="position:absolute; width:30px;  left:65px;  top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[8].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[8].run_time.time1 > 43200? '>12hrs': hw_values[8].run_time.time1 < 3600? new Date(hw_values[8].run_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[8].run_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:65px;  top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" :style="{color: hw_values[8].pump_schedule? '#c2c2c2':'grey'}">    <p >{{hw_values[8].off_time.time1 > 43200? '>12hrs': hw_values[8].off_time.time1 < 3600? new Date(hw_values[8].off_time.time1 * 1000).toISOString().substr(14, 5): new Date(hw_values[8].off_time.time1 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[8].run_time.time2 > 43200? '>12hrs': hw_values[8].run_time.time2 < 3600? new Date(hw_values[8].run_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[8].run_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:130px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[8].off_time.time2 > 43200? '>12hrs': hw_values[8].off_time.time2 < 3600? new Date(hw_values[8].off_time.time2 * 1000).toISOString().substr(14, 5): new Date(hw_values[8].off_time.time2 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[8].run_time.time3 > 43200? '>12hrs': hw_values[8].run_time.time3 < 3600? new Date(hw_values[8].run_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[8].run_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:195px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[8].off_time.time3 > 43200? '>12hrs': hw_values[8].off_time.time3 < 3600? new Date(hw_values[8].off_time.time3 * 1000).toISOString().substr(14, 5): new Date(hw_values[8].off_time.time3 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:7px;  color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[8].run_time.time4 > 43200? '>12hrs': hw_values[8].run_time.time4 < 3600? new Date(hw_values[8].run_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[8].run_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                            <div style="position:absolute; width:30px;  left:260px; top:32px; color:grey; display:flex; justify-content:flex-end; font-size:var(--font-size-medium);" >                                                                  <p >{{hw_values[8].off_time.time4 > 43200? '>12hrs': hw_values[8].off_time.time4 < 3600? new Date(hw_values[8].off_time.time4 * 1000).toISOString().substr(14, 5): new Date(hw_values[8].off_time.time4 * 1000).toISOString().substr(12, 7)}} </p></div>
                        </div> 
                    </div>



                    <!-- CYLINDER IMAGE -->
                    <div class="input-card" style="position:absolute; width:500px; left:0px; top:0px;"> 
                        <figure style="position:absolute; width:400px; left:368px; top:77px;"> <img style = "max-width:100%;" src="../../src/images/cylinder.png"> </img> </figure> 
                    </div>               


                    <!-- BOILER "CARD" -->
                    <div style="position:absolute; width:410px; height:58px; left:-50px; top:-30px; font-size:var(--font-size-medium)">
                        <div v-if="hw_values[8].pump_status"> <figure style="position:absolute; width:90px; left:303px; top:130px;"> <img style = "max-width:95%;" src="../../src/images/pump_on_supply.gif">  </img> </figure> </div>
                        <div v-else>                          <figure style="position:absolute; width:90px; left:303px; top:130px;"> <img style = "max-width:95%;" src="../../src/images/pump_off_supply.png"> </img> </figure> </div>
                        <div style="position:absolute; width:250px; left:314px; top:100px;" >  <p >  Boiler </p>    </div>
                        <div style="position:absolute; width:250px; left:352px; top:100px;" >  <p >  {{hw_values[10].actual}} C  </p>    </div>
                        <!-- BOILDER WATER FLOW -->
                        <div class="RotatePipe180" style="position:absolute; width:60px;  left:247px; top:165px;">  <b-progress :value="100" height="7"  :variant="hw_values[8].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[8].pump_status"></b-progress> </div>
                        <div class="RotatePipe180" style="position:absolute; width:142px; left:384px; top:142px;" > <b-progress :value="100" height="7"  :variant="hw_values[8].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[8].pump_status"></b-progress> </div>
                        <div                       style="position:absolute; width:7px;   left:523px; top:142px;" > <b-progress :value="100" height="65" :variant="hw_values[8].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[8].pump_status"></b-progress> </div>
                        <div                       style="position:absolute; width:295px; left:234px; top:203px;">  <b-progress :value="100" height="7"  :variant="hw_values[8].pump_status? 'hw-pipe-red':'hw-pipe-grey'" striped :animated="hw_values[8].pump_status"></b-progress> </div>
                    </div>

                </div>


                <!-- BOILER IMAGE -->
                <div class="input-card" style="position:absolute; width:500px; left:-30px; top:0px;"> 
                    <figure style="position:absolute; width:125px; left:100px; top:170px;"> <img style = "max-width:75%;" src="../../src/images/boiler.png">   </img> </figure> 
                </div>               



                <!-- CARD FOR USER INPUT SECTION AT BOTTOM -->
                <!-- SCHEDULE -->
                <div class="card" style="position:absolute; width:1280px; height:508px; left:30px;   top:550px; background-color:var(--background-colour-pump_false)"> </div> 
                <!-- TARGET TEMP -->
                <div class="card" style="position:absolute; width:330px;  height:508px; left:1320px; top:550px; background-color:var(--background-colour-pump_false)"> </div> 
                <!-- MANUAL OVERRIDE / BOOST -->
                <div class="card" style="position:absolute; width:215px;  height:508px; left:1660px; top:550px; background-color:var(--background-colour-pump_false)"> </div> 

                <div style="position:absolute; width:250px; left:650px;   top:560px; font-size:var(--font-size-xlarge); font-weight:bold;"> <p> Instant Hot Water Schedule </p>    </div>
                <div style="position:absolute; width:250px; left:1400px; top:560px;  font-size:var(--font-size-xlarge); font-weight:bold;"> <p> Temperature Setpoint </p>    </div>
                <div style="position:absolute; width:150px; left:1705px; top:560px;  font-size:var(--font-size-xlarge); font-weight:bold;"> <p> Manual Override </p>    </div>


                <!-- ****************** CURRENT TIME BAR ****************** -->
                <div class="card" style="position:absolute; left:185px; top:585px; backgroundColor:#1c1c1c;"> 
                    <div v-if="timeBar(0)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:5px;   top:10px; "></div>
                    <div v-if="timeBar(1)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:51px;  top:10px; "></div>
                    <div v-if="timeBar(2)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:97px;  top:10px; "></div>
                    <div v-if="timeBar(3)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:143px; top:10px; "></div>
                    <div v-if="timeBar(4)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:189px; top:10px; "></div>
                    <div v-if="timeBar(5)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:235px; top:10px; "></div>
                    <div v-if="timeBar(6)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:281px; top:10px; "></div>
                    <div v-if="timeBar(7)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:327px; top:10px; "></div>
                    <div v-if="timeBar(8)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:373px; top:10px; "></div>
                    <div v-if="timeBar(9)"  class="timer-card" style="position:absolute; width:40px; height:425px; left:419px; top:10px; "></div>
                    <div v-if="timeBar(10)" class="timer-card" style="position:absolute; width:40px; height:425px; left:465px; top:10px; "></div>
                    <div v-if="timeBar(11)" class="timer-card" style="position:absolute; width:40px; height:425px; left:511px; top:10px; "></div>
                    <div v-if="timeBar(12)" class="timer-card" style="position:absolute; width:40px; height:425px; left:557px; top:10px; "></div>
                    <div v-if="timeBar(13)" class="timer-card" style="position:absolute; width:40px; height:425px; left:603px; top:10px; "></div>
                    <div v-if="timeBar(14)" class="timer-card" style="position:absolute; width:40px; height:425px; left:649px; top:10px; "></div>
                    <div v-if="timeBar(15)" class="timer-card" style="position:absolute; width:40px; height:425px; left:695px; top:10px; "></div>
                    <div v-if="timeBar(16)" class="timer-card" style="position:absolute; width:40px; height:425px; left:741px; top:10px; "></div>
                    <div v-if="timeBar(17)" class="timer-card" style="position:absolute; width:40px; height:425px; left:787px; top:10px; "></div>
                    <div v-if="timeBar(18)" class="timer-card" style="position:absolute; width:40px; height:425px; left:833px; top:10px; "></div>
                    <div v-if="timeBar(19)" class="timer-card" style="position:absolute; width:40px; height:425px; left:879px; top:10px; "></div>
                    <div v-if="timeBar(20)" class="timer-card" style="position:absolute; width:40px; height:425px; left:925px; top:10px; "></div>
                    <div v-if="timeBar(21)" class="timer-card" style="position:absolute; width:40px; height:425px; left:969px; top:10px; "></div>
                    <div v-if="timeBar(22)" class="timer-card" style="position:absolute; width:40px; height:425px; left:1016px;top:10px; "></div>
                    <div v-if="timeBar(23)" class="timer-card" style="position:absolute; width:40px; height:425px; left:1063px;top:10px; "></div>
                </div>

                <!-- ****************** HEADER ****************** -->
                <div class="input-card" style="position:absolute; width:50px; left:180px; top:610px; font-size:var(--font-size-medium)"> 
                    <div style="position:absolute; width:250px; left:26px;   top:0px;" >   <p > 0 </p>    </div>
                    <div style="position:absolute; width:250px; left:72px;   top:0px;" >   <p > 1 </p>    </div>
                    <div style="position:absolute; width:250px; left:118px;  top:0px;" >   <p > 2 </p>    </div>
                    <div style="position:absolute; width:250px; left:164px;  top:0px;" >   <p > 3 </p>    </div>
                    <div style="position:absolute; width:250px; left:210px;  top:0px;" >   <p > 4 </p>    </div>
                    <div style="position:absolute; width:250px; left:256px;  top:0px;" >   <p > 5 </p>    </div>
                    <div style="position:absolute; width:250px; left:302px;  top:0px;" >   <p > 6 </p>    </div>
                    <div style="position:absolute; width:250px; left:348px;  top:0px;" >   <p > 7 </p>    </div>
                    <div style="position:absolute; width:250px; left:394px;  top:0px;" >   <p > 8 </p>    </div>
                    <div style="position:absolute; width:250px; left:440px;  top:0px;" >   <p > 9 </p>    </div>
                    <div style="position:absolute; width:250px; left:484px;  top:0px;" >   <p > 10 </p>    </div>
                    <div style="position:absolute; width:250px; left:530px;  top:0px;" >   <p > 11 </p>    </div>
                    <div style="position:absolute; width:250px; left:575px;  top:0px;" >   <p > 12 </p>    </div>
                    <div style="position:absolute; width:250px; left:621px;  top:0px;" >   <p > 13 </p>    </div>
                    <div style="position:absolute; width:250px; left:667px;  top:0px;" >   <p > 14 </p>    </div>
                    <div style="position:absolute; width:250px; left:713px;  top:0px;" >   <p > 15 </p>    </div>
                    <div style="position:absolute; width:250px; left:759px;  top:0px;" >   <p > 16 </p>    </div>
                    <div style="position:absolute; width:250px; left:805px;  top:0px;" >   <p > 17 </p>    </div>
                    <div style="position:absolute; width:250px; left:851px;  top:0px;" >   <p > 18 </p>    </div>
                    <div style="position:absolute; width:250px; left:897px;  top:0px;" >   <p > 19 </p>    </div>
                    <div style="position:absolute; width:250px; left:943px;  top:0px;" >   <p > 20 </p>    </div>
                    <div style="position:absolute; width:250px; left:989px;  top:0px;" >   <p > 21 </p>    </div>
                    <div style="position:absolute; width:250px; left:1035px; top:0px;" >   <p > 22 </p>    </div>
                    <div style="position:absolute; width:250px; left:1081px; top:0px;" >   <p > 23 </p>    </div>
                    <div style="position:absolute; width:100px; left:1170px; top:0px;" >   <p > Zone </p> </div>
                    <div style="position:absolute; width:100px; left:1250px; top:0px;" >   <p > Target C </p> </div>
                    <div style="position:absolute; width:100px; left:1530px; top:0px;" >   <p > Boost </p> </div>
                    <div style="position:absolute; width:100px; left:1615px; top:0px;" >   <p > Timer </p> </div>
                    
                    <div style="position:absolute; width:250px; left:26px;   top:20px;" >   <p > {{curr_hour == 0? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:72px;   top:20px;" >   <p > {{curr_hour == 1? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:118px;  top:20px;" >   <p > {{curr_hour == 2? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:164px;  top:20px;" >   <p > {{curr_hour == 3? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:210px;  top:20px;" >   <p > {{curr_hour == 4? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:256px;  top:20px;" >   <p > {{curr_hour == 5? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:302px;  top:20px;" >   <p > {{curr_hour == 6? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:348px;  top:20px;" >   <p > {{curr_hour == 7? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:394px;  top:20px;" >   <p > {{curr_hour == 8? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:440px;  top:20px;" >   <p > {{curr_hour == 9? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:484px;  top:20px;" >   <p > {{curr_hour == 10? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:530px;  top:20px;" >   <p > {{curr_hour == 11? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:575px;  top:20px;" >   <p > {{curr_hour == 12? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:621px;  top:20px;" >   <p > {{curr_hour == 13? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:667px;  top:20px;" >   <p > {{curr_hour == 14? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:713px;  top:20px;" >   <p > {{curr_hour == 15? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:759px;  top:20px;" >   <p > {{curr_hour == 16? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:805px;  top:20px;" >   <p > {{curr_hour == 17? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:851px;  top:20px;" >   <p > {{curr_hour == 18? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:897px;  top:20px;" >   <p > {{curr_hour == 19? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:943px;  top:20px;" >   <p > {{curr_hour == 20? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:989px;  top:20px;" >   <p > {{curr_hour == 21? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:1035px; top:20px;" >   <p > {{curr_hour == 22? curr_mins:''}}  </p>    </div>
                    <div style="position:absolute; width:250px; left:1081px; top:20px;" >   <p > {{curr_hour == 23? curr_mins:''}}  </p>    </div>

                    <!-- CYLINDER USER INPUT - CHANGE TEMP -->
                    <div style="position:absolute; width:70px; left:1165px;  top:408px;" > Cylinder </div>
                    <div style="position:absolute; width:70px; left:1260px;  top:408px;" > {{hw_values[9].target}} C </div>
                    <div style="position:absolute; width:70px; left:1325px;  top:404px;" > <button v-on:click="changeTargetTemp(9, -0.5)"> -0.5 </button> </div> 
                    <div style="position:absolute; width:70px; left:1395px;  top:404px;" > <button v-on:click="changeTargetTemp(9, +0.5)"> +0.5 </button> </div> 
                </div>

                <!-- **************************** KITCHEN **************************** -->
                <div class="input-card" style="position:absolute; width:50px; left:180px; top:610px; font-size:var(--font-size-medium)"> 
                    <div style="position:absolute; width:250px; left:-130px; top:65px; font-size:110%;" >  <p > Kitchen </p>    </div>
                    <div style="position:absolute; width:250px; left:1165px; top:65px; font-size:110%;" >  <p > Kitchen </p>    </div>
                    <div style="position:absolute; width:250px; left:-36px;  top:55px; font-size:var(--font-size-medium);" >   <p > 00-30 </p>    </div>
                    <div style="position:absolute; width:250px; left:-36px;  top:87px; font-size:var(--font-size-medium);" >   <p > 30-60 </p>    </div>
                    <div style="position:absolute; width:50px; left:10px;   top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','0','status00_30')"  :style="{backgroundColor: curr_hour ==  0 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[0].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:56px;   top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','1','status00_30')"  :style="{backgroundColor: curr_hour ==  1 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[1].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:102px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','2','status00_30')"  :style="{backgroundColor: curr_hour ==  2 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[2].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:148px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','3','status00_30')"  :style="{backgroundColor: curr_hour ==  3 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[3].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:194px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','4','status00_30')"  :style="{backgroundColor: curr_hour ==  4 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[4].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:240px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','5','status00_30')"  :style="{backgroundColor: curr_hour ==  5 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[5].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:286px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','6','status00_30')"  :style="{backgroundColor: curr_hour ==  6 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[6].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:332px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','7','status00_30')"  :style="{backgroundColor: curr_hour ==  7 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[7].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:378px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','8','status00_30')"  :style="{backgroundColor: curr_hour ==  8 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[8].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:424px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','9','status00_30')"  :style="{backgroundColor: curr_hour ==  9 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[9].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:470px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','10','status00_30')" :style="{backgroundColor: curr_hour == 10 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[10].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:516px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','11','status00_30')" :style="{backgroundColor: curr_hour == 11 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[11].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:562px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','12','status00_30')" :style="{backgroundColor: curr_hour == 12 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[12].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:608px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','13','status00_30')" :style="{backgroundColor: curr_hour == 13 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[13].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:654px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','14','status00_30')" :style="{backgroundColor: curr_hour == 14 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[14].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:700px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','15','status00_30')" :style="{backgroundColor: curr_hour == 15 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[15].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:746px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','16','status00_30')" :style="{backgroundColor: curr_hour == 16 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[16].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:792px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','17','status00_30')" :style="{backgroundColor: curr_hour == 17 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[17].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:838px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','18','status00_30')" :style="{backgroundColor: curr_hour == 18 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[18].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:884px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','19','status00_30')" :style="{backgroundColor: curr_hour == 19 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[19].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:930px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','20','status00_30')" :style="{backgroundColor: curr_hour == 20 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[20].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:976px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','21','status00_30')" :style="{backgroundColor: curr_hour == 21 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[21].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1022px; top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','22','status00_30')" :style="{backgroundColor: curr_hour == 22 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[22].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1068px; top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','23','status00_30')" :style="{backgroundColor: curr_hour == 23 && curr_mins < 31 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[23].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:10px;   top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','0','status30_60')"  :style="{backgroundColor: curr_hour ==  0 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[0].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:56px;   top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','1','status30_60')"  :style="{backgroundColor: curr_hour ==  1 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[1].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:102px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','2','status30_60')"  :style="{backgroundColor: curr_hour ==  2 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[2].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:148px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','3','status30_60')"  :style="{backgroundColor: curr_hour ==  3 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[3].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:194px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','4','status30_60')"  :style="{backgroundColor: curr_hour ==  4 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[4].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:240px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','5','status30_60')"  :style="{backgroundColor: curr_hour ==  5 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[5].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:286px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','6','status30_60')"  :style="{backgroundColor: curr_hour ==  6 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[6].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:332px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','7','status30_60')"  :style="{backgroundColor: curr_hour ==  7 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[7].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:378px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','8','status30_60')"  :style="{backgroundColor: curr_hour ==  8 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[8].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:424px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','9','status30_60')"  :style="{backgroundColor: curr_hour ==  9 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[9].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:470px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','10','status30_60')" :style="{backgroundColor: curr_hour == 10 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[10].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:516px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','11','status30_60')" :style="{backgroundColor: curr_hour == 11 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[11].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:562px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','12','status30_60')" :style="{backgroundColor: curr_hour == 12 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[12].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:608px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','13','status30_60')" :style="{backgroundColor: curr_hour == 13 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[13].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:654px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','14','status30_60')" :style="{backgroundColor: curr_hour == 14 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[14].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:700px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','15','status30_60')" :style="{backgroundColor: curr_hour == 15 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[15].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:746px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','16','status30_60')" :style="{backgroundColor: curr_hour == 16 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[16].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:792px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','17','status30_60')" :style="{backgroundColor: curr_hour == 17 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[17].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:838px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','18','status30_60')" :style="{backgroundColor: curr_hour == 18 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[18].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:884px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','19','status30_60')" :style="{backgroundColor: curr_hour == 19 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[19].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:930px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','20','status30_60')" :style="{backgroundColor: curr_hour == 20 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[20].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:976px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','21','status30_60')" :style="{backgroundColor: curr_hour == 21 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[21].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1022px; top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','22','status30_60')" :style="{backgroundColor: curr_hour == 22 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[22].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1068px; top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_kitchen','23','status30_60')" :style="{backgroundColor: curr_hour == 23 && curr_mins > 30 && hw_values[0].override_status?'var(--override-button-colour)':hw_schedule_kitchen[23].status30_60?'green':''}"  > . </button> </div>
                    <!-- TARGET TEMP -->
                    <div style="position:absolute; width:100px; left:1260px;  top:65px;" >   <p>{{hw_values[1].target}} C</p> </div>
                    <div style="position:absolute; width:70px;  left:1325px;  top:61px;" >   <button v-on:click="changeTargetTemp(1, -0.5)"> -0.5 </button> </div>
                    <div style="position:absolute; width:70px;  left:1395px;  top:61px;" >   <button v-on:click="changeTargetTemp(1, +0.5)"> +0.5 </button> </div>
                     <!-- MANUAL OVERRIDE -->
                    <div style="position:absolute; width:100px; left:1510px;  top:65px;" >   <button v-on:click="toggleOverride('Heating Central/Pump - Kitchen',0)" :style="{backgroundColor: hw_values[0].override_status?'var(--override-button-colour)':''}"> . </button> </div>
                    <div style="position:absolute; width:100px; left:1620px;  top:69px; font-size:var(--font-size-large);" >   <p> {{hw_values[0].override_timer >0? new Date(hw_values[0].override_timer * 1000).toISOString().substr(14, 5) : ''}} </p></div>
               </div>



                <!-- **************************** MASTER **************************** -->
                <div class="input-card" style="position:absolute; width:50px; left:180px; top:700px; font-size:var(--font-size-medium)"> 
                    <div style="position:absolute; width:250px; left:-130px; top:65px; font-size:110%;" >  <p > Master</p>    </div>
                    <div style="position:absolute; width:250px; left:1165px; top:65px; font-size:110%;" >  <p > Master</p>    </div>
                    <div style="position:absolute; width:250px; left:-36px;  top:55px; font-size:var(--font-size-medium);" >   <p > 00-30 </p>    </div>
                    <div style="position:absolute; width:250px; left:-36px;  top:87px; font-size:var(--font-size-medium);" >   <p > 30-60 </p>    </div>
                    <div style="position:absolute; width:50px; left:10px;   top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','0','status00_30')"  :style="{backgroundColor: curr_hour ==  0 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[0].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:56px;   top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','1','status00_30')"  :style="{backgroundColor: curr_hour ==  1 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[1].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:102px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','2','status00_30')"  :style="{backgroundColor: curr_hour ==  2 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[2].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:148px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','3','status00_30')"  :style="{backgroundColor: curr_hour ==  3 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[3].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:194px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','4','status00_30')"  :style="{backgroundColor: curr_hour ==  4 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[4].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:240px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','5','status00_30')"  :style="{backgroundColor: curr_hour ==  5 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[5].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:286px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','6','status00_30')"  :style="{backgroundColor: curr_hour ==  6 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[6].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:332px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','7','status00_30')"  :style="{backgroundColor: curr_hour ==  7 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[7].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:378px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','8','status00_30')"  :style="{backgroundColor: curr_hour ==  8 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[8].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:424px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','9','status00_30')"  :style="{backgroundColor: curr_hour ==  9 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[9].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:470px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','10','status00_30')" :style="{backgroundColor: curr_hour == 10 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[10].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:516px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','11','status00_30')" :style="{backgroundColor: curr_hour == 11 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[11].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:562px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','12','status00_30')" :style="{backgroundColor: curr_hour == 12 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[12].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:608px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','13','status00_30')" :style="{backgroundColor: curr_hour == 13 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[13].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:654px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','14','status00_30')" :style="{backgroundColor: curr_hour == 14 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[14].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:700px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','15','status00_30')" :style="{backgroundColor: curr_hour == 15 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[15].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:746px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','16','status00_30')" :style="{backgroundColor: curr_hour == 16 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[16].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:792px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','17','status00_30')" :style="{backgroundColor: curr_hour == 17 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[17].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:838px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','18','status00_30')" :style="{backgroundColor: curr_hour == 18 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[18].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:884px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','19','status00_30')" :style="{backgroundColor: curr_hour == 19 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[19].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:930px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','20','status00_30')" :style="{backgroundColor: curr_hour == 20 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[20].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:976px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','21','status00_30')" :style="{backgroundColor: curr_hour == 21 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[21].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1022px; top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','22','status00_30')" :style="{backgroundColor: curr_hour == 22 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[22].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1068px; top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','23','status00_30')" :style="{backgroundColor: curr_hour == 23 && curr_mins < 31 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[23].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:10px;   top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','0','status30_60')"  :style="{backgroundColor: curr_hour ==  0 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[0].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:56px;   top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','1','status30_60')"  :style="{backgroundColor: curr_hour ==  1 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[1].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:102px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','2','status30_60')"  :style="{backgroundColor: curr_hour ==  2 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[2].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:148px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','3','status30_60')"  :style="{backgroundColor: curr_hour ==  3 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[3].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:194px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','4','status30_60')"  :style="{backgroundColor: curr_hour ==  4 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[4].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:240px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','5','status30_60')"  :style="{backgroundColor: curr_hour ==  5 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[5].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:286px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','6','status30_60')"  :style="{backgroundColor: curr_hour ==  6 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[6].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:332px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','7','status30_60')"  :style="{backgroundColor: curr_hour ==  7 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[7].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:378px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','8','status30_60')"  :style="{backgroundColor: curr_hour ==  8 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[8].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:424px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','9','status30_60')"  :style="{backgroundColor: curr_hour ==  9 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[9].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:470px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','10','status30_60')" :style="{backgroundColor: curr_hour == 10 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[10].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:516px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','11','status30_60')" :style="{backgroundColor: curr_hour == 11 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[11].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:562px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','12','status30_60')" :style="{backgroundColor: curr_hour == 12 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[12].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:608px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','13','status30_60')" :style="{backgroundColor: curr_hour == 13 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[13].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:654px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','14','status30_60')" :style="{backgroundColor: curr_hour == 14 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[14].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:700px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','15','status30_60')" :style="{backgroundColor: curr_hour == 15 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[15].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:746px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','16','status30_60')" :style="{backgroundColor: curr_hour == 16 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[16].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:792px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','17','status30_60')" :style="{backgroundColor: curr_hour == 17 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[17].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:838px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','18','status30_60')" :style="{backgroundColor: curr_hour == 18 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[18].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:884px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','19','status30_60')" :style="{backgroundColor: curr_hour == 19 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[19].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:930px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','20','status30_60')" :style="{backgroundColor: curr_hour == 20 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[20].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:976px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','21','status30_60')" :style="{backgroundColor: curr_hour == 21 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[21].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1022px; top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','22','status30_60')" :style="{backgroundColor: curr_hour == 22 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[22].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1068px; top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_master','23','status30_60')" :style="{backgroundColor: curr_hour == 23 && curr_mins > 30 && hw_values[2].override_status?'var(--override-button-colour)':hw_schedule_master[23].status30_60?'green':''}"  > . </button> </div>

                    <!-- TARGET TEMP -->
                    <div style="position:absolute; width:100px; left:1260px;  top:65px;" >   <P>{{hw_values[3].target}} C</P> </div>
                    <div style="position:absolute; width:70px;  left:1325px;  top:61px;" >   <button v-on:click="changeTargetTemp(3, -0.5)"> -0.5 </button> </div>
                    <div style="position:absolute; width:70px;  left:1395px;  top:61px;" >   <button v-on:click="changeTargetTemp(3, +0.5)"> +0.5 </button> </div>
                    <!-- MANUAL OVERRIDE -->
                    <div style="position:absolute; width:100px; left:1510px;  top:65px;" >   <button id="x"   v-on:click="toggleOverride('Heating Central/Pump - Master',2)" :style="{backgroundColor: hw_values[2].override_status?'var(--override-button-colour)':''}"> . </button> </div>
                    <div style="position:absolute; width:100px; left:1620px;  top:69px; font-size:var(--font-size-large);" >   <p> {{hw_values[2].override_timer >0? new Date(hw_values[2].override_timer * 1000).toISOString().substr(14, 5) : ''}} </p></div>
                </div>

                <!-- **************************** LOFT / 1ST FLOOR **************************** -->
                <div class="input-card" style="position:absolute; width:50px; left:180px; top:790px; font-size:var(--font-size-medium)"> 
                    <div style="position:absolute; width:250px; left:-130px; top:65px; font-size:110%;" >  <p > 1st / Loft </p>    </div>
                    <div style="position:absolute; width:250px; left:1165px; top:65px; font-size:110%;" >  <p > 1st / Loft </p>    </div>
                    <div style="position:absolute; width:250px; left:-36px;  top:55px; font-size:var(--font-size-medium);" >   <p > 00-30 </p>    </div>
                    <div style="position:absolute; width:250px; left:-36px;  top:87px; font-size:var(--font-size-medium);" >   <p > 30-60 </p>    </div>
                    <div style="position:absolute; width:50px; left:10px;   top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','0','status00_30')"  :style="{backgroundColor: curr_hour ==  0 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[0].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:56px;   top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','1','status00_30')"  :style="{backgroundColor: curr_hour ==  1 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[1].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:102px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','2','status00_30')"  :style="{backgroundColor: curr_hour ==  2 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[2].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:148px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','3','status00_30')"  :style="{backgroundColor: curr_hour ==  3 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[3].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:194px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','4','status00_30')"  :style="{backgroundColor: curr_hour ==  4 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[4].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:240px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','5','status00_30')"  :style="{backgroundColor: curr_hour ==  5 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[5].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:286px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','6','status00_30')"  :style="{backgroundColor: curr_hour ==  6 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[6].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:332px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','7','status00_30')"  :style="{backgroundColor: curr_hour ==  7 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[7].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:378px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','8','status00_30')"  :style="{backgroundColor: curr_hour ==  8 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[8].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:424px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','9','status00_30')"  :style="{backgroundColor: curr_hour ==  9 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[9].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:470px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','10','status00_30')" :style="{backgroundColor: curr_hour == 10 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[10].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:516px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','11','status00_30')" :style="{backgroundColor: curr_hour == 11 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[11].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:562px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','12','status00_30')" :style="{backgroundColor: curr_hour == 12 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[12].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:608px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','13','status00_30')" :style="{backgroundColor: curr_hour == 13 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[13].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:654px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','14','status00_30')" :style="{backgroundColor: curr_hour == 14 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[14].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:700px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','15','status00_30')" :style="{backgroundColor: curr_hour == 15 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[15].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:746px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','16','status00_30')" :style="{backgroundColor: curr_hour == 16 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[16].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:792px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','17','status00_30')" :style="{backgroundColor: curr_hour == 17 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[17].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:838px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','18','status00_30')" :style="{backgroundColor: curr_hour == 18 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[18].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:884px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','19','status00_30')" :style="{backgroundColor: curr_hour == 19 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[19].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:930px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','20','status00_30')" :style="{backgroundColor: curr_hour == 20 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[20].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:976px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','21','status00_30')" :style="{backgroundColor: curr_hour == 21 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[21].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1022px; top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','22','status00_30')" :style="{backgroundColor: curr_hour == 22 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[22].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1068px; top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','23','status00_30')" :style="{backgroundColor: curr_hour == 23 && curr_mins < 31 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[23].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:10px;   top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','0','status30_60')"  :style="{backgroundColor: curr_hour ==  0 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[0].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:56px;   top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','1','status30_60')"  :style="{backgroundColor: curr_hour ==  1 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[1].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:102px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','2','status30_60')"  :style="{backgroundColor: curr_hour ==  2 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[2].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:148px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','3','status30_60')"  :style="{backgroundColor: curr_hour ==  3 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[3].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:194px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','4','status30_60')"  :style="{backgroundColor: curr_hour ==  4 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[4].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:240px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','5','status30_60')"  :style="{backgroundColor: curr_hour ==  5 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[5].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:286px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','6','status30_60')"  :style="{backgroundColor: curr_hour ==  6 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[6].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:332px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','7','status30_60')"  :style="{backgroundColor: curr_hour ==  7 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[7].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:378px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','8','status30_60')"  :style="{backgroundColor: curr_hour ==  8 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[8].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:424px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','9','status30_60')"  :style="{backgroundColor: curr_hour ==  9 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[9].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:470px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','10','status30_60')" :style="{backgroundColor: curr_hour == 10 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[10].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:516px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','11','status30_60')" :style="{backgroundColor: curr_hour == 11 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[11].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:562px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','12','status30_60')" :style="{backgroundColor: curr_hour == 12 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[12].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:608px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','13','status30_60')" :style="{backgroundColor: curr_hour == 13 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[13].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:654px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','14','status30_60')" :style="{backgroundColor: curr_hour == 14 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[14].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:700px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','15','status30_60')" :style="{backgroundColor: curr_hour == 15 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[15].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:746px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','16','status30_60')" :style="{backgroundColor: curr_hour == 16 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[16].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:792px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','17','status30_60')" :style="{backgroundColor: curr_hour == 17 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[17].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:838px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','18','status30_60')" :style="{backgroundColor: curr_hour == 18 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[18].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:884px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','19','status30_60')" :style="{backgroundColor: curr_hour == 19 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[19].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:930px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','20','status30_60')" :style="{backgroundColor: curr_hour == 20 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[20].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:976px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','21','status30_60')" :style="{backgroundColor: curr_hour == 21 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[21].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1022px; top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','22','status30_60')" :style="{backgroundColor: curr_hour == 22 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[22].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1068px; top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_1stloft','23','status30_60')" :style="{backgroundColor: curr_hour == 23 && curr_mins > 30 && hw_values[4].override_status?'var(--override-button-colour)':hw_schedule_1stloft[23].status30_60?'green':''}"  > . </button> </div>
                    <!-- TARGET TEMP -->
                    <div style="position:absolute; width:100px; left:1260px;  top:65px;" >   <P>{{hw_values[5].target}} C</P> </div>
                    <div style="position:absolute; width:70px;  left:1325px;  top:61px;" >   <button v-on:click="changeTargetTemp(5, -0.5)"> -0.5 </button> </div>
                    <div style="position:absolute; width:70px;  left:1395px;  top:61px;" >   <button v-on:click="changeTargetTemp(5, +0.5)"> +0.5 </button> </div>
                    <!-- MANUAL OVERRIDE -->
                    <div style="position:absolute; width:100px; left:1510px;  top:65px;" >   <button id="x"   v-on:click="toggleOverride('Heating Central/Pump - 1st-Loft',4)" :style="{backgroundColor: hw_values[4].override_status?'var(--override-button-colour)':''}"> . </button> </div>
                    <div style="position:absolute; width:100px; left:1620px;  top:69px; font-size:var(--font-size-large);" >   <p> {{hw_values[4].override_timer >0? new Date(hw_values[4].override_timer * 1000).toISOString().substr(14, 5) : ''}} </p></div>
              </div>

                <!-- **************************** GARDEN **************************** -->
                <div class="input-card" style="position:absolute; width:50px; left:180px; top:880px; font-size:var(--font-size-medium)"> 
                    <div style="position:absolute; width:250px; left:-130px; top:65px; font-size:110%;" >  <p > Garden </p>    </div>
                    <div style="position:absolute; width:250px; left:1165px; top:65px; font-size:110%;" >  <p > Garden </p>    </div>
                    <div style="position:absolute; width:250px; left:-36px;  top:55px; font-size:var(--font-size-medium);" >   <p > 00-30 </p>    </div>
                    <div style="position:absolute; width:250px; left:-36px;  top:87px; font-size:var(--font-size-medium);" >   <p > 30-60 </p>    </div>

                    <div style="position:absolute; width:50px; left:10px;   top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','0','status00_30')"  :style="{backgroundColor: curr_hour ==  0 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[0].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:56px;   top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','1','status00_30')"  :style="{backgroundColor: curr_hour ==  1 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[1].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:102px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','2','status00_30')"  :style="{backgroundColor: curr_hour ==  2 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[2].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:148px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','3','status00_30')"  :style="{backgroundColor: curr_hour ==  3 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[3].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:194px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','4','status00_30')"  :style="{backgroundColor: curr_hour ==  4 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[4].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:240px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','5','status00_30')"  :style="{backgroundColor: curr_hour ==  5 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[5].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:286px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','6','status00_30')"  :style="{backgroundColor: curr_hour ==  6 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[6].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:332px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','7','status00_30')"  :style="{backgroundColor: curr_hour ==  7 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[7].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:378px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','8','status00_30')"  :style="{backgroundColor: curr_hour ==  8 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[8].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:424px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','9','status00_30')"  :style="{backgroundColor: curr_hour ==  9 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[9].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:470px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','10','status00_30')" :style="{backgroundColor: curr_hour == 10 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[10].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:516px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','11','status00_30')" :style="{backgroundColor: curr_hour == 11 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[11].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:562px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','12','status00_30')" :style="{backgroundColor: curr_hour == 12 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[12].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:608px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','13','status00_30')" :style="{backgroundColor: curr_hour == 13 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[13].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:654px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','14','status00_30')" :style="{backgroundColor: curr_hour == 14 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[14].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:700px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','15','status00_30')" :style="{backgroundColor: curr_hour == 15 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[15].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:746px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','16','status00_30')" :style="{backgroundColor: curr_hour == 16 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[16].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:792px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','17','status00_30')" :style="{backgroundColor: curr_hour == 17 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[17].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:838px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','18','status00_30')" :style="{backgroundColor: curr_hour == 18 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[18].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:884px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','19','status00_30')" :style="{backgroundColor: curr_hour == 19 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[19].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:930px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','20','status00_30')" :style="{backgroundColor: curr_hour == 20 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[20].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:976px;  top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','21','status00_30')" :style="{backgroundColor: curr_hour == 21 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[21].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1022px; top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','22','status00_30')" :style="{backgroundColor: curr_hour == 22 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[22].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1068px; top:50px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','23','status00_30')" :style="{backgroundColor: curr_hour == 23 && curr_mins < 31 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[23].status00_30?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:10px;   top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','0','status30_60')"  :style="{backgroundColor: curr_hour ==  0 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[0].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:56px;   top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','1','status30_60')"  :style="{backgroundColor: curr_hour ==  1 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[1].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:102px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','2','status30_60')"  :style="{backgroundColor: curr_hour ==  2 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[2].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:148px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','3','status30_60')"  :style="{backgroundColor: curr_hour ==  3 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[3].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:194px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','4','status30_60')"  :style="{backgroundColor: curr_hour ==  4 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[4].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:240px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','5','status30_60')"  :style="{backgroundColor: curr_hour ==  5 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[5].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:286px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','6','status30_60')"  :style="{backgroundColor: curr_hour ==  6 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[6].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:332px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','7','status30_60')"  :style="{backgroundColor: curr_hour ==  7 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[7].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:378px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','8','status30_60')"  :style="{backgroundColor: curr_hour ==  8 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[8].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:424px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','9','status30_60')"  :style="{backgroundColor: curr_hour ==  9 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[9].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:470px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','10','status30_60')" :style="{backgroundColor: curr_hour == 10 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[10].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:516px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','11','status30_60')" :style="{backgroundColor: curr_hour == 11 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[11].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:562px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','12','status30_60')" :style="{backgroundColor: curr_hour == 12 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[12].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:608px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','13','status30_60')" :style="{backgroundColor: curr_hour == 13 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[13].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:654px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','14','status30_60')" :style="{backgroundColor: curr_hour == 14 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[14].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:700px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','15','status30_60')" :style="{backgroundColor: curr_hour == 15 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[15].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:746px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','16','status30_60')" :style="{backgroundColor: curr_hour == 16 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[16].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:792px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','17','status30_60')" :style="{backgroundColor: curr_hour == 17 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[17].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:838px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','18','status30_60')" :style="{backgroundColor: curr_hour == 18 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[18].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:884px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','19','status30_60')" :style="{backgroundColor: curr_hour == 19 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[19].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:930px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','20','status30_60')" :style="{backgroundColor: curr_hour == 20 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[20].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:976px;  top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','21','status30_60')" :style="{backgroundColor: curr_hour == 21 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[21].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1022px; top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','22','status30_60')" :style="{backgroundColor: curr_hour == 22 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[22].status30_60?'green':''}"  > . </button> </div>
                    <div style="position:absolute; width:50px; left:1068px; top:82px;" >   <button id="x"   v-on:click="changeTimer('hw_schedule_garden','23','status30_60')" :style="{backgroundColor: curr_hour == 23 && curr_mins > 30 && hw_values[6].override_status?'var(--override-button-colour)':hw_schedule_garden[23].status30_60?'green':''}"  > . </button> </div>
                    <!-- TARGET TEMP -->
                    <div style="position:absolute; width:100px; left:1260px;  top:65px;" >   <P>{{hw_values[7].target}} C</P> </div>
                    <div style="position:absolute; width:70px;  left:1325px;  top:61px;" >   <button v-on:click="changeTargetTemp(7, -0.5)"> -0.5 </button> </div>
                    <div style="position:absolute; width:70px;  left:1395px;  top:61px;" >   <button v-on:click="changeTargetTemp(7, +0.5)"> +0.5 </button> </div>
                    <!-- MANUAL OVERRIDE -->
                    <div style="position:absolute; width:100px; left:1510px;  top:65px;" >   <button id="x"   v-on:click="toggleOverride('Heating Central/Pump - Garden',6)" :style="{backgroundColor: hw_values[6].override_status?'var(--override-button-colour)':''}"> . </button> </div>
                    <div style="position:absolute; width:100px; left:1620px;  top:69px; font-size:var(--font-size-large);" >   <p> {{hw_values[6].override_timer >0? new Date(hw_values[6].override_timer * 1000).toISOString().substr(14, 5) : ''}} </p></div>
              </div>

            </template>
        </div>
    </b-container>

</template>




<script> 
// import ProgressBar from 'vue-progressbar-component'
import { GChart } from "vue-google-charts";

export default {
    name: "HotWater",
  
 components: {
//       ProgressBar,
         GChart,
     },

    data() {
        return {

        curr_time:0,
        curr_hour:0,
        curr_mins:0,

        runtimeCalcultor_flag:false,              //calculates seconds since pump started - flag used to manage setInterval within timer function
        offimeCalcultor_flag:false,               //calculates seconds since pump stopped - flag used to manage setInterval within timer function
        manualOverrideTimer_flag: false,          //calculates seconds manual override started - flag used to manage setInterval within timer function

        hw_timer:{
            hw_schedule_1stloft:false,
            hw_schedule_kitchen:false,
            hw_schedule_garden:false,
            hw_schedule_master:false,
        },
        
        hw_values: [
            {device:"Heating Central/Pump - Kitchen",           pump_status:false,  pump_schedule:false,    override_start_time:0,    override_status:false,    override_timer:0,
                                                                                    run_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}, 
                                                                                    off_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}},
            {device:"Heating Central/Temp Kitchen Return",      actual:25,          target:20},

            {device:"Heating Central/Pump - Master",            pump_status:false,  pump_schedule:false,    override_start_time:0,    override_status:false,    override_timer:0,      
                                                                                    run_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}, 
                                                                                    off_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}},
            {device:"Heating Central/Temp MasterWC Return",     actual:25,          target:20},

            {device:"Heating Central/Pump - 1st-Loft",          pump_status:false,  pump_schedule:false,    override_start_time:0,    override_status:false,    override_timer:0,      
                                                                                    run_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}, 
                                                                                    off_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}},
            {device:"Heating Central/Temp 1st-Loft Return",     actual:25,          target:20},

            {device:"Heating Central/Pump - Garden",            pump_status:false,  pump_schedule:false,    override_start_time:0,    override_status:false,    override_timer:0,      
                                                                                    run_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}, 
                                                                                    off_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}},
            {device:"Heating Central/Temp Garden Return",       actual:25,          target:20},

            {device:"Heating Central/B4_Hot Water",             pump_status:false,  pump_schedule:false,      
                                                                                    run_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}, 
                                                                                    off_time:{time1:0, time2:0, time3:0, time4:0, start_time:new Date()}},

            {device:"Heating Central/Temp Cylinder Supply",     actual:25,          target:20},
            {device:"Heating Central/Temp Boiler Supply",       actual:25},    
            {device:"System_Data",                              manual_override_time:1800, max_run_time_pump:360, max_run_time_boilder:1200, delta_C:3.5},    
        ],

        hw_schedule_1stloft:
            [
            {hour:"0",       status00_30:false,        status30_60:false}, {hour:"1",       status00_30:false,        status30_60:false}, {hour:"2",       status00_30:false,        status30_60:false}, {hour:"3",       status00_30:false,        status30_60:false},
            {hour:"4",       status00_30:false,        status30_60:false}, {hour:"5",       status00_30:false,        status30_60:false}, {hour:"6",       status00_30:false,        status30_60:false}, {hour:"7",       status00_30:true,         status30_60:true},            
            {hour:"8",       status00_30:true,         status30_60:true},  {hour:"9",       status00_30:true,         status30_60:true},  {hour:"10",      status00_30:false,        status30_60:false}, {hour:"11",      status00_30:false,        status30_60:false},            
            {hour:"12",      status00_30:false,        status30_60:false}, {hour:"13",      status00_30:false,        status30_60:false}, {hour:"14",      status00_30:false,        status30_60:false}, {hour:"15",      status00_30:false,        status30_60:false},            
            {hour:"16",      status00_30:false,        status30_60:false}, {hour:"17",      status00_30:false,        status30_60:true},  {hour:"18",      status00_30:true,         status30_60:true}, {hour:"19",      status00_30:true,         status30_60:true},            
            {hour:"20",      status00_30:false,        status30_60:false}, {hour:"21",      status00_30:false,        status30_60:false}, {hour:"22",      status00_30:false,        status30_60:false}, {hour:"23",      status00_30:false,        status30_60:false},            
            {hour:"24",      status00_30:false,        status30_60:false},            
            ],

        hw_schedule_kitchen:
            [
            {hour:"0",       status00_30:false,        status30_60:false}, {hour:"1",       status00_30:false,        status30_60:false}, {hour:"2",       status00_30:false,        status30_60:false}, {hour:"3",       status00_30:false,        status30_60:false},
            {hour:"4",       status00_30:false,        status30_60:false}, {hour:"5",       status00_30:false,        status30_60:false}, {hour:"6",       status00_30:false,        status30_60:false}, {hour:"7",       status00_30:true,         status30_60:true},            
            {hour:"8",       status00_30:true,         status30_60:true},  {hour:"9",       status00_30:true,         status30_60:true},  {hour:"10",      status00_30:false,        status30_60:false}, {hour:"11",      status00_30:false,        status30_60:false},            
            {hour:"12",      status00_30:false,        status30_60:false}, {hour:"13",      status00_30:false,        status30_60:false}, {hour:"14",      status00_30:false,        status30_60:false}, {hour:"15",      status00_30:false,        status30_60:false},            
            {hour:"16",      status00_30:false,        status30_60:false}, {hour:"17",      status00_30:false,        status30_60:true},  {hour:"18",      status00_30:true,         status30_60:true}, {hour:"19",      status00_30:true,         status30_60:true},            
            {hour:"20",      status00_30:false,        status30_60:false}, {hour:"21",      status00_30:false,        status30_60:false}, {hour:"22",      status00_30:false,        status30_60:false}, {hour:"23",      status00_30:false,        status30_60:false},            
            {hour:"24",      status00_30:false,        status30_60:false},               
            ],

        hw_schedule_master:
            [
            {hour:"0",       status00_30:false,        status30_60:false}, {hour:"1",       status00_30:false,        status30_60:false}, {hour:"2",       status00_30:false,        status30_60:false}, {hour:"3",       status00_30:false,        status30_60:false},
            {hour:"4",       status00_30:false,        status30_60:false}, {hour:"5",       status00_30:false,        status30_60:false}, {hour:"6",       status00_30:false,        status30_60:false}, {hour:"7",       status00_30:true,         status30_60:true},            
            {hour:"8",       status00_30:true,         status30_60:true},  {hour:"9",       status00_30:true,         status30_60:true},  {hour:"10",      status00_30:false,        status30_60:false}, {hour:"11",      status00_30:false,        status30_60:false},            
            {hour:"12",      status00_30:false,        status30_60:false}, {hour:"13",      status00_30:false,        status30_60:false}, {hour:"14",      status00_30:false,        status30_60:false}, {hour:"15",      status00_30:false,        status30_60:false},            
            {hour:"16",      status00_30:false,        status30_60:false}, {hour:"17",      status00_30:false,        status30_60:true},  {hour:"18",      status00_30:true,         status30_60:true}, {hour:"19",      status00_30:true,         status30_60:true},            
            {hour:"20",      status00_30:false,        status30_60:false}, {hour:"21",      status00_30:false,        status30_60:false}, {hour:"22",      status00_30:false,        status30_60:false}, {hour:"23",      status00_30:false,        status30_60:false},            
            {hour:"24",      status00_30:false,        status30_60:false},               
            ],

        hw_schedule_garden:
            [
            {hour:"0",       status00_30:false,        status30_60:false}, {hour:"1",       status00_30:false,        status30_60:false}, {hour:"2",       status00_30:false,        status30_60:false}, {hour:"3",       status00_30:false,        status30_60:false},
            {hour:"4",       status00_30:false,        status30_60:false}, {hour:"5",       status00_30:false,        status30_60:false}, {hour:"6",       status00_30:false,        status30_60:false}, {hour:"7",       status00_30:true,         status30_60:true},            
            {hour:"8",       status00_30:true,         status30_60:true},  {hour:"9",       status00_30:true,         status30_60:true},  {hour:"10",      status00_30:false,        status30_60:false}, {hour:"11",      status00_30:false,        status30_60:false},            
            {hour:"12",      status00_30:false,        status30_60:false}, {hour:"13",      status00_30:false,        status30_60:false}, {hour:"14",      status00_30:false,        status30_60:false}, {hour:"15",      status00_30:false,        status30_60:false},            
            {hour:"16",      status00_30:false,        status30_60:false}, {hour:"17",      status00_30:false,        status30_60:true},  {hour:"18",      status00_30:true,         status30_60:true}, {hour:"19",      status00_30:true,         status30_60:true},            
            {hour:"20",      status00_30:false,        status30_60:false}, {hour:"21",      status00_30:false,        status30_60:false}, {hour:"22",      status00_30:false,        status30_60:false}, {hour:"23",      status00_30:false,        status30_60:false},            
            {hour:"24",      status00_30:false,        status30_60:false},               
            ],

       
        }
    },


    methods: {

    changeTimer: function(schedule,hour,mins){
        var current_status = this[schedule][hour][mins]
        //console.log("current status = ", current_status, schedule, hour, mins)
        // this[schedule][hour][mins] = !current_status

        uibuilder.send({
            'page': "hotwater",
            'type': "schedule_update",
            'variable_name': schedule,
            'hour': hour,
            'mins': mins,
            'status_update': !current_status,
            })
    },

    changeTargetTemp: function(object_pos,temp_adj){
        var current_target = this.hw_values[object_pos].target

        uibuilder.send({
            'page': "hotwater",
            'type': "device_data_update",
            'variable_name': "hw_values",
            'object_position': object_pos,
            'property': 'target',
            'value': current_target + temp_adj,
            })
    },

    varianceTarget: function(object_pos){
        var current_target  = this.hw_values[object_pos].target
        var current_actual  = this.hw_values[object_pos].actual
        var variance        = current_actual - current_target
        variance            = variance.toFixed(1)
        var sign            = variance > 0? "+" : ""
        return sign + variance
    },



    timeBar: function(input_hour){
        var date        = new Date()
        var hours       = date.getHours()
        this.curr_hour  = hours
        this.curr_mins  = this.format24()
        var time        = new Date();
        var hour        = time.getHours();
        var min         = time.getMinutes();
        var visible     = input_hour == hour? true : false
        return visible
    },

    format24: function() {
        var date        = new Date()
        var hours       = date.getHours()
        var minutes     = date.getMinutes()
        hours           = hours ? hours : 12; // the hour '0' should be '12'
        hours           = hours 
        minutes         = minutes < 10 ? '0'+minutes : minutes
        var strTime = minutes 
        return strTime
    },

    //termparature bar charts per pump/zone
    tempProgressBar: function (temp) {
        const min_temp  = 40
        const factor    = 8.33             //40 + 12 = 52 --- calclate as 100/12
        var ProgressBarValue = (temp - min_temp)*factor
        ProgressBarValue = ProgressBarValue < 0 ? 1 : ProgressBarValue
        ProgressBarValue = ProgressBarValue > 100 ? 100 : ProgressBarValue
        return ProgressBarValue
    },


   runtimeCalcultor: function () {
        if (this.runtimeCalcultor_flag === false)
            {
            this.runtimeCalcultor_flag = setInterval(function(){
                var date = new Date()
                date = date.getTime()
                var hw_values = this.hw_values
                this.hw_values[0].run_time.time1 = this.hw_values[0].run_time.start_time > 0? Number(((date - this.hw_values[0].run_time.start_time)/1000).toFixed(0))  : this.hw_values[0].run_time.time1
                this.hw_values[2].run_time.time1 = this.hw_values[2].run_time.start_time > 0? Number(((date - this.hw_values[2].run_time.start_time)/1000).toFixed(0))  : this.hw_values[2].run_time.time1
                this.hw_values[4].run_time.time1 = this.hw_values[4].run_time.start_time > 0? Number(((date - this.hw_values[4].run_time.start_time)/1000).toFixed(0))  : this.hw_values[4].run_time.time1
                this.hw_values[6].run_time.time1 = this.hw_values[6].run_time.start_time > 0? Number(((date - this.hw_values[6].run_time.start_time)/1000).toFixed(0))  : this.hw_values[6].run_time.time1
                this.hw_values[8].run_time.time1 = this.hw_values[8].run_time.start_time > 0? Number(((date - this.hw_values[8].run_time.start_time)/1000).toFixed(0))  : this.hw_values[8].run_time.time1
            if (this.hw_values[0].pump_status === false && this.hw_values[2].pump_status === false && this.hw_values[4].pump_status === false && this.hw_values[6].pump_status === false && this.hw_values[8].pump_status === false) 
                {
                clearInterval(this.runtimeCalcultor_flag)
                this.runtimeCalcultor_flag = false
                }
            }.bind(this), 1000);
            }
   },

   offtimeCalcultor: function () {
        if (this.offimeCalcultor_flag === false)
            {
            this.offimeCalcultor_flag = setInterval(function(){
                var date = new Date()
                date = date.getTime() 
                var hw_values = this.hw_values
                this.hw_values[0].off_time.time1 = this.hw_values[0].off_time.start_time > 0? Number(((date - this.hw_values[0].off_time.start_time)/1000).toFixed(0))  : this.hw_values[0].off_time.time1
                this.hw_values[2].off_time.time1 = this.hw_values[2].off_time.start_time > 0? Number(((date - this.hw_values[2].off_time.start_time)/1000).toFixed(0))  : this.hw_values[2].off_time.time1
                this.hw_values[4].off_time.time1 = this.hw_values[4].off_time.start_time > 0? Number(((date - this.hw_values[4].off_time.start_time)/1000).toFixed(0))  : this.hw_values[4].off_time.time1
                this.hw_values[6].off_time.time1 = this.hw_values[6].off_time.start_time > 0? Number(((date - this.hw_values[6].off_time.start_time)/1000).toFixed(0))  : this.hw_values[6].off_time.time1
                this.hw_values[8].off_time.time1 = this.hw_values[8].off_time.start_time > 0? Number(((date - this.hw_values[8].off_time.start_time)/1000).toFixed(0))  : this.hw_values[8].off_time.time1

                if (this.hw_values[0].pump_status === true && this.hw_values[2].pump_status === true && this.hw_values[4].pump_status === true && this.hw_values[6].pump_status === true && this.hw_values[8].pump_status === true) 
                    {
                    clearInterval(this.offimeCalcultor_flag)
                    this.offimeCalcultor_flag = false
                    }
            }.bind(this), 1000);
            }
   },

    toggleOverride: function(device,object_pos) {

        var date = new Date()
        date = date.getTime()
        var hw_values   = this.hw_values
        hw_values       = hw_values.find(hw => hw.device == device);

        //console.log("stgatus = ", device, hw_values.override_status)
        hw_values.override_status = !hw_values.override_status
        hw_values.override_start_time = hw_values.override_status == true? date : 0

        //console.log("stgatus = ", device, hw_values.override_status, hw_values.override_start_time)

        //send override time node-red03
        uibuilder.send({
            'page': "hotwater",
            'type': "device_data_update",
            'variable_name': "hw_values",
            'object_position': object_pos,
            'property': 'override_start_time',
            'value': hw_values.override_start_time,
            })

        //send override status to node-red
        uibuilder.send({
            'page': "hotwater",
            'type': "device_data_update",
            'variable_name': "hw_values",
            'object_position': object_pos,
            'property': 'override_status',
            'value': hw_values.override_status,
            })


    },

    //timer to calculate the time left from a manual override
    manualOverrideTimer: function () {

        if (this.manualOverrideTimer_flag === false)
            {
            this.manualOverrideTimer_flag = setInterval(function(){
                var date = new Date()
                date = date.getTime() 
                var hw_values = this.hw_values
                var total_time = hw_values[11].manual_override_time

                // calculate time left on override
                this.hw_values[0].override_timer = this.hw_values[0].override_status? Number((total_time - (date - this.hw_values[0].override_start_time)/1000).toFixed(0))  : this.hw_values[0].override_timer
                this.hw_values[2].override_timer = this.hw_values[2].override_status? Number((total_time - (date - this.hw_values[2].override_start_time)/1000).toFixed(0))  : this.hw_values[2].override_timer
                this.hw_values[4].override_timer = this.hw_values[4].override_status? Number((total_time - (date - this.hw_values[4].override_start_time)/1000).toFixed(0))  : this.hw_values[4].override_timer
                this.hw_values[6].override_timer = this.hw_values[6].override_status? Number((total_time - (date - this.hw_values[6].override_start_time)/1000).toFixed(0))  : this.hw_values[6].override_timer

                //On completion of timer - update override status variable to FALSE and send new status to Node-RED
                if (Number((total_time - (date - this.hw_values[0].override_start_time)/1000).toFixed(0)) <0) {this.hw_values[0].override_status = false; this.manualOverrideFinished(0)} 
                if (Number((total_time - (date - this.hw_values[2].override_start_time)/1000).toFixed(0)) <0) {this.hw_values[2].override_status = false; this.manualOverrideFinished(2)} 
                if (Number((total_time - (date - this.hw_values[4].override_start_time)/1000).toFixed(0)) <0) {this.hw_values[4].override_status = false; this.manualOverrideFinished(4)} 
                if (Number((total_time - (date - this.hw_values[6].override_start_time)/1000).toFixed(0)) <0) {this.hw_values[6].override_status = false; this.manualOverrideFinished(6)} 
  
                //stop this function if no override in play
                if (this.hw_values[0].override_status === false && this.hw_values[2].override_status === false && this.hw_values[4].override_status === false && this.hw_values[6].override_status === false) 
                    {
                    clearInterval(this.manualOverrideTimer_flag)
                    this.manualOverrideTimer_flag = false
                    }
            }.bind(this), 1000);
            }
        },

        manualOverrideFinished: function (object_pos){
            //send override status to node-red
            uibuilder.send({
                'page': "hotwater",
                'type': "device_data_update",
                'variable_name': "hw_values",
                'object_position': object_pos,
                'property': 'override_status',
                'value': false,
                })


        },



    //removes the relevant property from the Node_RED incoming hw_values so as to not overwrite the constantly changing on/off timer per pump/zone
    updatehw_values: function(hw_values){
        var temp = hw_values
        temp[0].off_time.time1 = temp[0].off_time.start_time > 0?  this.hw_values[0].off_time.time1 : temp[0].off_time.time1
        temp[2].off_time.time1 = temp[2].off_time.start_time > 0?  this.hw_values[2].off_time.time1 : temp[2].off_time.time1
        temp[4].off_time.time1 = temp[4].off_time.start_time > 0?  this.hw_values[4].off_time.time1 : temp[4].off_time.time1
        temp[6].off_time.time1 = temp[6].off_time.start_time > 0?  this.hw_values[6].off_time.time1 : temp[6].off_time.time1
        temp[8].off_time.time1 = temp[8].off_time.start_time > 0?  this.hw_values[8].off_time.time1 : temp[8].off_time.time1
        
        temp[0].run_time.time1 = temp[0].run_time.start_time > 0?  this.hw_values[0].run_time.time1 : temp[0].run_time.time1
        temp[2].run_time.time1 = temp[2].run_time.start_time > 0?  this.hw_values[2].run_time.time1 : temp[2].run_time.time1
        temp[4].run_time.time1 = temp[4].run_time.start_time > 0?  this.hw_values[4].run_time.time1 : temp[4].run_time.time1
        temp[6].run_time.time1 = temp[6].run_time.start_time > 0?  this.hw_values[6].run_time.time1 : temp[6].run_time.time1
        temp[8].run_time.time1 = temp[8].run_time.start_time > 0?  this.hw_values[8].run_time.time1 : temp[8].run_time.time1
        
        temp[0].override_timer = temp[0].override_status?          this.hw_values[0].override_timer : temp[0].override_timer
        temp[2].override_timer = temp[2].override_status?          this.hw_values[2].override_timer : temp[2].override_timer
        temp[4].override_timer = temp[4].override_status?          this.hw_values[4].override_timer : temp[4].override_timer
        temp[6].override_timer = temp[6].override_status?          this.hw_values[6].override_timer : temp[6].override_timer
        this.hw_values           = temp
    },


    //Refresh entire floorplan page
    reloadPage(){
    window.location.reload()
    },


},

    // Start-up
    mounted() {

        // **REQUIRED** Start uibuilder comms with Node-RED
        // Also required as the new model has turned off <keep-alive> in App.vue, so pages that are not in focus are not kept alive, meaning newly opened pages need a new connection to uibuilder*/
        uibuilder.start('/home', '/uibuilder/vendor/socket.io')
        //console.log("router = ",this.$route)

        // msg is updated when a standard msg is received from Node-RED
        uibuilder.onChange('msg', (msg) => {
                
        //only run code if correct message type has been received
        if (msg.page == "hotwater" && this.$route.path == "/HotWater") {                            
            //update variables             
            if (msg.hw_values        != undefined)  {this.updatehw_values(msg.hw_values)}
            if (msg.schedule_1stloft != undefined)  {this.hw_schedule_1stloft = msg.schedule_1stloft}
            if (msg.schedule_kitchen != undefined)  {this.hw_schedule_kitchen = msg.schedule_kitchen}
            if (msg.schedule_master  != undefined)  {this.hw_schedule_master  = msg.schedule_master}
            if (msg.schedule_garden  != undefined)  {this.hw_schedule_garden  = msg.schedule_garden}
        }

        //runtime calculation - show current run time for any pump that is currently running or duration of stop time
        if (this.hw_values[0].pump_status === true ||  this.hw_values[2].pump_status === true ||  this.hw_values[4].pump_status === true ||  this.hw_values[6].pump_status === true ||  this.hw_values[8].pump_status === true) {this.runtimeCalcultor()}
        if (this.hw_values[0].pump_status === false || this.hw_values[2].pump_status === false || this.hw_values[4].pump_status === false || this.hw_values[6].pump_status === false || this.hw_values[8].pump_status === false) {this.offtimeCalcultor()}

        //manual override timer - start the timer if manual override has been set for any zone
        if (this.hw_values[0].override_status === true || this.hw_values[2].override_status === true || this.hw_values[4].override_status === true || this.hw_values[6].override_status === true)  {this.manualOverrideTimer()}

        })
    }
}

</script>



<style>

:root{

  /* ***************** HOTWATER ***************** */
  --background-colour-timer: #303030;                   /* schedule card colour */
  --background-colour-pump_true: #303030;               /* individual pump temps card colour */
  --background-colour-pump_false: #212020;              /* individual pump temps card colour */
  --background-colour-progress-bar: #212020;            /* individual pump progress bar background colour */
  --background-colour-delta-progress-bar: #212020;      /* individual pump progress bar background colour - delta only */
  --override-button-colour: #d10606;
  --colour-temp-rhs-pipes: #7d7d7d;                     /* individual pump temps on RHS on top of water pipes */


}

/* varaints for progress bar */
.bg-hw-pipe-red{
    background-color: #eb2c1e !important;
}
.bg-hw-pipe-grey{
    background-color: grey !important;
}
.bg-hw-pipe-blue{
    background-color: #007bff !important;
}

</style>



<style lang="scss" scoped>

.timer-card{
    font-size:105%;
    background-color:var(--background-colour-timer); 
}
.RotatePipe180{
    transform:rotate(180deg);
}
.RotatePipe90{
    transform:rotate(90deg);
}
.b-progress {
  background-color:transparent !important;
  -webkit-box-shadow: none;
  box-shadow: none;
}
.target-process{
  background-color:none !important;
  -webkit-box-shadow: none;
  box-shadow: none;
  color:#404040;
}

</style>
