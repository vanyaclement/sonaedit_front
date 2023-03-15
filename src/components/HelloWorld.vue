<template>
  <v-data-table
    :headers="headers"
    :items="desserts"
    class="elevation-1 text-center"
  >
    <template v-slot:item="{ item }">
      <tr>
        <td class="bAll">
          <!-- <v-checkbox
            v-model="selected1"
            :single-select="singleSelected1"
            show-select
          ></v-checkbox> -->
          <!-- <v-btn @click="deleteRow(selected[0].name)">Delete Selected</v-btn> -->

          <v-btn
            color="indigo"
            dark
            v-on:click="nextPage(item)"
            class="buttons-me"
          >
            Delete
          </v-btn>

          <v-progress-linear
            color="deep-purple accent-4"
            indeterminate
            rounded
            class="buttons-me"
          ></v-progress-linear>

          <template>
            <div class="text-center" id="edit-btn">
              <v-menu
                v-model="menu"
                :close-on-content-click="false"
                :nudge-width="200"
                offset-x
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-btn
                    color="indigo"
                    dark
                    v-bind="attrs"
                    v-on="on"
                    class="buttons-me"
                  >
                    Edit
                  </v-btn>
                </template>

                <v-card id="edit-card">
                  <!-- <form id="edit-form" @submit="editlog(item)" method="put"> -->
                  <!-- <input type="text" name="model"  placeholder="" v-model="editform.model" ><br>
                    <button type="submit">Edit</button> -->
                  <form @submit="editlog(item)" method="put">
                    <div class="d-flex flex-row">
                      <div class="form-group col-md-6 edit-lg3">
                        <label>Model</label>
                        <input
                          type="text"
                          class="form-control"
                          id="inputEmail4"
                          placeholder="model"
                          v-model="model"
                        
                        />
                        <v-btn text color="primary" @click="$refs.menu15.save(model)"></v-btn>
                        

                      </div>
                      <div class="form-group col-md-6 edit-lg2">
                        <label>PartNo</label>
                        <input
                          type="text"
                          class="form-control"
                          id="inputPassword4"
                          placeholder="partno"
                          v-model="part_number"
                        />
                        <v-btn text color="primary" @click="$refs.menu16.save(part_number)"></v-btn>
                      </div>
                      <div class="form-group col-md-6 edit-lg1">
                        <label>Project_type</label>
                        <input
                          type="text"
                          class="form-control"
                          id="inputAddress"
                          placeholder="project_type"
                          v-model="project_type"
                        />
                        <v-btn text color="primary" @click="$refs.menu17.save(project_type)"></v-btn>
                      </div>
                    </div>
                    <div class="d-flex flex-row">
                      <div class="form-group col-md-6 edit-lg3">
                        <label>Quantity</label>
                        <input
                          type="text"
                          class="form-control"
                          id="inputPassword4"
                          placeholder="quantity"
                          v-model="quantity"
                        />
                        <v-btn text color="primary" @click="$refs.menu18.save(quantity)"></v-btn>
                      </div>
                      <div class="form-group col-md-6 edit-lg2">
                        <label>Priority</label>
                        <input
                          type="text"
                          class="form-control"
                          id="inputPassword4"
                          
                          placeholder="priority"
                          v-model="priority"
                        />
                        <v-btn text color="primary" @click="$refs.menu19.save(priority)"></v-btn>
                      </div>
                    </div>
                    <div class="d-flex flex-row">
                      <div class="form-group col-md-6 edit-lg3">
                        <label>Status</label>
                        <input
                          type="text"
                          class="form-control"
                          id="inputPassword4"
                          placeholder="status"
                          v-model="status"
                        />
                        <v-btn text color="primary" @click="$refs.menu20.save(status)"></v-btn>
                      </div>
                      <div class="form-group col-md-6 edit-lg2">
                        <v-col>
                          <v-menu
                            ref="menu"
                            v-model="menu"
                            :close-on-content-click="false"
                            transition="scale-transition"
                            offset-y
                            min-width="auto"
                          >
                            <template v-slot:activator="{ on, attrs }">
                              <v-text-field
                                v-model="startD"
                                label="Start Date "
                                prepend-icon="mdi-calendar"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-date-picker
                              v-model="startD">
                              <v-btn text color="primary" @click="menu13 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu13.save(startD)">Ok</v-btn>


                            </v-date-picker>
                          </v-menu>
                        </v-col>
                      </div>
                      <div class="form-group col-md-6 edit-lg1">
                        <v-col>
                          <v-menu
                            ref="menu"
                            v-model="menu"
                            :close-on-content-click="false"
                            transition="scale-transition"
                            offset-y
                            min-width="auto"
                          >
                            <template v-slot:activator="{ on, attrs }">
                              <v-text-field
                                v-model="endD"
                                label="End Date "
                                prepend-icon="mdi-calendar"
                                readonly
                                v-bind="attrs"
                                v-on="on"
                              ></v-text-field>
                            </template>
                            <v-date-picker
                              v-model="endD">
                              <v-btn text color="primary" @click="menu14 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu14.save(endD)">Ok</v-btn>
                            </v-date-picker>
                          </v-menu>
                        </v-col>
                      </div>
                    </div>
                  
                    

                    <button type="submit" class="btn btn-primary edit-submit">
                      submit
                    </button>
                  </form>

                  <!-- <div class="card-body">
                              <div class="form-group">
                                <input type="text" class="form-control" id="put-id" placeholder="Id">
                              </div>
                              <div class="form-group">
                                <input type="text" class="form-control" id="put-title" placeholder="Title">
                              </div>
                              <div class="form-group">
                                <input type="text" class="form-control" id="put-description" placeholder="Description">
                              </div>
                              
                              <div class="form-group mt-2">
                                <button class="btn btn-sm btn-primary" onclick="editlog(item)">Update Data</button>
                               
                              </div>

                              <div id="putResult"></div>
                            </div> -->
                </v-card>
              </v-menu>
            </div>
          </template>
        </td>

        <!-- <i  @click="deleteRow(index)" class="fa fa-remove" style="font-size:25px;color:red;cursor:pointer"></i> -->

        <td class="bAll">{{ item.model }}</td>
        <td class="bAll">{{ item.part_number }}</td>
        <td class="bAll">{{ item.project_type }}</td>
        <td class="bAll">{{ item.quantity }}</td>
        <td class="bAll">{{ item.priority }}</td>
        <!-- STATUS  -->
        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.status}}</td>
          </tr>
          <tr>
            <td class="bBottom layout">Actual</td>
          </tr>
          <tr>
            <td class="layout">Remark</td>
          </tr>
        </td>

        <!-- START DATE  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.start_p }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">2023-01-19</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- END DATE  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.end_p }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">2023-01-26</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- NUMBER OF DAYS  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.days }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- % COMPLETED  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.completed }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- KICK OFF -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.kicks }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- DRAWING  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.approvalDate }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- STEEL MASTER  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.steelDate }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- DIE DESIGN  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.designDate }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- JIGS DESIGN  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.jigsDate }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- BROACH  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.broachDate }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- GUAGES  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.GuagesDate }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- FORGING  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.forgingDate }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- SOFT MACHINE  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.softDate }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- HEAT TREATMENT  -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.heatDate }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- QG4 -->

        <td class="bAll">
          <tr>
            <td class="bBottom layout">{{ item.qg4Date }}</td>
          </tr>
          <tr>
            <td class="bBottom layout">--</td>
          </tr>
          <tr>
            <td class="layout">--</td>
          </tr>
        </td>

        <!-- <td class="text-center">
<v-icon small class="mr-2" @click="editItem(item)">
  mdi-pencil
</v-icon>
</td> -->
      </tr>
    </template>
    <template v-slot:top>
      <v-toolbar flat>
        <v-toolbar-title>NPD PROJECT STATUS SHEET </v-toolbar-title>
        <v-divider class="mx-4" inset vertical></v-divider>
        <!-- <v-text-field v-model="search" append-icon="mdi-magnify" label="Search" single-line hide-details></v-text-field> -->
        <v-spacer></v-spacer>

        <v-dialog v-model="dialog">
          <template v-slot:activator="{ on, attrs }">
            <v-btn color="primary" dark class="mb-2" v-bind="attrs" v-on="on">
              ADD DATA
            </v-btn>
            <!-- <v-btn
              color="primary"
              dark
              class="mb-2 mr-2"
              @click="edit(selected1)"
            >
              <v-icon small class="mr-1">mdi-pencil</v-icon> EDIT DATA
            </v-btn> -->
          </template>
          <v-card>
            <v-card-title class="text-h5 grey lighten-2">
              ADD DATA HERE
            </v-card-title>

            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="postdata.model"
                      label="Model"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="postdata.part_number"
                      type="number"
                      label="Part Number"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-autocomplete
                      v-model="postdata.project_type"
                      :items="type"
                      label="Project Type"
                      placeholder="Select..."
                    >
                    </v-autocomplete>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="postdata.quantity"
                      type="number"
                      label="Quantity"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-autocomplete
                      v-model="postdata.priority"
                      :items="priority_type"
                      label="Priority"
                      placeholder="Select..."
                    >
                    </v-autocomplete>
                  </v-col>
                </v-row>

                <!-- STATUS FOR PLAN  -->
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-autocomplete
                      v-model="postdata.status_p"
                      :items="status_p"
                      label="Status"
                      placeholder="Select..."
                    >
                    </v-autocomplete>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on }">
                        <v-text-field
                          v-model="startDate"
                          label="Start Date "
                          prepend-icon="mdi-calendar"
                          readonly
                       
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="startDate" scrollable>
                        <v-spacer></v-spacer>
                        <v-btn text color="primary" @click="menu1 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.dialog.save(startDate)">Ok</v-btn>
                      
                      
                      </v-date-picker>
                    </v-menu>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="endDate"
                          label="End Date "
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="endDate" :min="startDate">
                        <v-btn text color="primary" @click="menu2 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu2.save(endDate)">Ok</v-btn>

                      
                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- DRAWING  -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on }">
                        <v-text-field
                          v-model="approvalDate"
                          label="Drawing Approval from customer"
                          prepend-icon="mdi-calendar"
                          readonly
                         
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="approvalDate">
                        <v-btn text color="primary" @click="menu3 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu2.save(approvalDate)">Ok</v-btn>

                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- STEEL  -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on }">
                        <v-text-field
                          v-model="steelDate"
                          label="Steel master release"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="steelDate">
                        <v-btn text color="primary" @click="menu4 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu2.save(steelDate)">Ok</v-btn>
                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- DIE DESIGN  -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on }">
                        <v-text-field
                          v-model="designDate"
                          label="Die Design & Drawing Release"
                          prepend-icon="mdi-calendar"
                          readonly
                         
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="designDate">
                        <v-btn text color="primary" @click="menu5 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu5.save(designDate)">Ok</v-btn>

                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- Jigs Design & drawing release -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{on}">
                        <v-text-field
                          v-model="jigsDate"
                          label="Jigs Desiign and Drawing Release"
                          prepend-icon="mdi-calendar"
                          readonly
                          
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="jigsDate">
                        <v-btn text color="primary" @click="menu6 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu6.save(jigsDate)">Ok</v-btn>

                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- BROACH  -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="broachDate"
                          label="BROACH Manufacturing"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="broachDate">
                      <v-btn text color="primary" @click="menu7 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu7.save(broachDate)">Ok</v-btn>
                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- GUAGES  -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="GuagesDate"
                          label="GUAGES Drawing Release"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="GuagesDate">
                        <v-btn text color="primary" @click="menu8= false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu8.save(GuagesDate)">Ok</v-btn>

                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- FORGING  -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="forgingDate"
                          label="Forging"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="forgingDate">
                        <v-btn text color="primary" @click="menu9 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu9.save(forgingDate)">Ok</v-btn>

                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- SOFT  -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="softDate"
                          label="Soft Machining"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="softDate">
                        <v-btn text color="primary" @click="menu10 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu10.save(softDate)">Ok</v-btn>

                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- HEAT TREATMENT  -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="heatDate"
                          label="Heat Treatment"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="heatDate">
                        <v-btn text color="primary" @click="menu11 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu11.save(heatDate)">Ok</v-btn>

                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                <!-- QG4 -->

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="qg4Date"
                          label="QG4"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="qg4Date">
                        <v-btn text color="primary" @click="menu12 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu12.save(qg4Date)">Ok</v-btn>

                      </v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>
              </v-container>
            </v-card-text>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="dialog = false">
                Cancel
              </v-btn>
              <v-btn color="blue darken-1" text @click="save()"> Save </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>

        <!-- dialogue 2  -->

     <!---- <v-dialog v-model="dialog1">
          <v-card>
            <v-card-title class="text-h5 grey lighten-2">
              Update DATA HERE
            </v-card-title>
            <v-card-text>
              <v-container>
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editdata.model"
                      label="Model"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editdata.part_number"
                      type="number"
                      label="Part Number"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-autocomplete
                      v-model="editdata.project_type"
                      :items="type"
                      label="Project Type"
                      placeholder="Select..."
                    >
                    </v-autocomplete>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-text-field
                      v-model="editdata.quantity"
                      type="number"
                      label="Quantity"
                    ></v-text-field>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-autocomplete
                      v-model="editdata.priority"
                      :items="priority_type"
                      label="Priority"
                      placeholder="Select..."
                    >
                    </v-autocomplete>
                  </v-col>
                </v-row>

               
                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-autocomplete
                      v-model="editdata.status_p"
                      :items="status_p"
                      label="Status"
                      placeholder="Select..."
                    >
                    </v-autocomplete>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="startD"
                          label="Start Date "
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="starD">
                        <v-btn text color="primary" @click="menu13 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu13.save(startD)">Ok</v-btn>

                      </v-date-picker>
                    </v-menu>
                  </v-col>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="endD"
                          label="End Date "
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="endD">
                        <v-btn text color="primary" @click="menu14 = false">Cancel</v-btn>
                        <v-btn text color="primary" @click="$refs.menu14.save(endD)">Ok</v-btn>
                      </v-date-picker>
                  
                      
                    </v-menu>
                  </v-col>
                </v-row>

               

            <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="date"
                          label="Drawing Approval from customer"
                          prepend-icon="event"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="date" no-title @input ="menu1= false"></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

               

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="editdata.steel"
                          label="Steel master release"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="editdata.steel"
                        :active-picker.sync="activePicker"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="editdata.die"
                          label="Die Design & Drawing Release"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="editdata.die"
                        :active-picker.sync="activePicker"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

               

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="editdata.jigs"
                          label="Jigs Desiign and Drawing Release"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="editdata.jigs"
                        :active-picker.sync="activePicker"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="editdata.broach"
                          label="BROACH Manufacturing"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="editdata.broach"
                        :active-picker.sync="activePicker"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

                

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="editdata.gauges"
                          label="GUAGES Drawing Release"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="editdata.gauges"
                        :active-picker.sync="activePicker"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

              

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="editdata.forging"
                          label="Forging"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="editdata.forging"
                        :active-picker.sync="activePicker"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

               

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="editdata.soft"
                          label="Soft Machining"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="editdata.soft"
                        :active-picker.sync="activePicker"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

       

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="editdata.heat"
                          label="Heat Treatment"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="editdata.heat"
                        :active-picker.sync="activePicker"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>

               

                <v-row>
                  <v-col cols="12" sm="6" md="4">
                    <v-menu
                      ref="menu"
                      v-model="menu"
                      :close-on-content-click="false"
                      transition="scale-transition"
                      offset-y
                      min-width="auto"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="editdata.qg"
                          label="QG4"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker
                        v-model="editdata.qg"
                        :active-picker.sync="activePicker"
                      ></v-date-picker>
                    </v-menu>
                  </v-col>
                </v-row>  
              </v-container>
            </v-card-text> 

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn color="blue darken-1" text @click="dialog1 = false">
                Cancel
              </v-btn>
              <v-btn color="blue darken-1" text @click="update()">
                UPDATE
              </v-btn>
            </v-card-actions>
          </v-card>
        </v-dialog>  -->
      </v-toolbar>
    </template>
  </v-data-table>
</template>

<script>
import axios from "axios";

export default {
  datadog() {
    return {
      id: '',
      app :{
      startDate:null,
      endDate:null,
      approvalDate:null,
      steelDate:null,
      designDate:null,
      jigsDate:null,
      broachDate:null,
      GuagesDate:null,
      forgingDate:null,
      softDate:null,
      heatDate:null,
      qg4Date:null,
      startD:null,
      endD:null,
      model:null,
      part_number:null,
      project_type:null,
      quantity:null,
      priority:null,
      status:null,
      menu1: false,
      menu2:false,
      menu3:false,
      menu4:false,
      menu5:false,
      menu6: false,
      menu7:false,
      menu8:false,
      menu9:false,
      menu10: false,
      menu11:false,
      menu12:false,
      menu13:false,
      menu14:false,
      menu15:false,
      menu16:false,
      menu17:false,
      menu18:false,
      menu19:false,
      menu20:false,
     }
      };
  },

  form: {
    model: "",
  },
  data: () => ({
    select: { state: "" },
    selected1: [],
    singleSelect1: true,

    search: "",
    status_p: ["Plan"],
    status_a: ["Actual"],
    status_r: ["Remark"],
    priority_type: ["H", "M", "L"],
    type: ["A", "B", "C", "D"],
    dialog: false,
    dialog1: false,

     dialogDelete: false,

   desserts: [],
    editedIndex: "",
    postdata: {
      model: "",
      part_number: "",
       project_type: "",
       quantity: "",
       priority: "",
       status: "",
       startD: "",
       endD: "",
      
     },

     //defaultItem: {
     //  model: "",
       //part_number: "",
       //project_type: "",
      // quantity: "",
     //  priority: "",
       //status_p: "",
       //start_p: "",
      // end_p: "",
      // days: "",
      // completed: "",
       //kicks: "",
        //drawing: "",
      // steel: "",
      // die: "",
      // jigs: "",
       //broach: "",
      // gauges: "",
      // forging: "",
       //soft: "",
       //heat: "",
       //qg: "",
   //  },
    // editedItem: {
     //  model: "",
    //   part_number: "",
     //  project_type: "",
     //  quantity: "",
     //  priority: "",
     //  status_p: "Actual",
     //  start_p: "",
     //  end_p: "",
     //  days: "",
     //  completed: "",
      // kicks: "",
      // drawing: "",
      // steel: "",
       //die: "",
     //  jigs: "",
     //  broach: "",
      // gauges: "",
     //  forging: "",
     //  soft: "",
      // heat: "",
     //  qg: "",
    // }, 
   /* editdata: {
      model: "",
      part_number: "",
      project_type: "",
      quantity: "",
      priority: "",
      status: "",
      startD: "",
      endD: "",
      
    }, */
   /*  editform: {
       model: null,
      part_number: null,
       project_type: null,
       quantity: null,
       priority: null,
       status: null,
       startD: null,
       endD: null,
      
      }, */
  }), 

  computed: {
    headers() {
      return [
        {
          text: "Select",
          value: "",
          sortable: false,
          class: "table_border text-center ",
        },
        {
          text: "Model",
          value: "model",
          sortable: false,
          class: "table_border text-center ",
        },
        {
          text: "Part No.",
          value: "part_number",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Project Type",
          value: "project_type",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Quantity",
          value: "quantity",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Priority",
          value: "priority",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Status",
          value: "status",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Start Date",
          value: "startD",
          sortable: false,
          class: "table_border",
        },
        {
          text: "End Date",
          value: "endD",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Number of Days",
          value: "days",
          sortable: false,
          class: "table_border",
        },
        {
          text: "%Completed",
          value: "completed",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Kick off",
          value: "kicks",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Drawing Approval From Customer",
          value: "drawing",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Steel Master Release",
          value: "steel",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Die Design & Drawing Release",
          value: "die",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Jigs Design & drawing release",
          value: "jigs",
          sortable: false,
          class: "table_border",
        },
        {
          text: "BROACH  manufacturing",
          value: "broach",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Gauges Drawing Release",
          value: "gauges",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Forging(QG-1)",
          value: "forging",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Soft Machining",
          value: "soft",
          sortable: false,
          class: "table_border",
        },
        {
          text: "Heat Treatment",
          value: "heat",
          sortable: false,
          class: "table_border",
        },
        { text: "QG4", value: "qg", sortable: false, class: "table_border" },
        // { text: 'Actions', value: 'actions', sortable: false ,class:"table_border"}
      ];
    },
  }, 

  mounted() {
    this.getapicall();
  },

  methods: {
   nextPage: function (item) {
      console.log();

       axios
        .delete(`http://localhost:8080/api/items/${item.model}`)
        .then((result) => {
          console.log("Result : ", result);
          this.getapicall();
          this.postdata = {};
          console.log("deleted data ");
        })
        .catch((err) => {
          console.log("Error : ", err);
        }); 
    },
    editlog: function (item) {
      console.log(item.model);
      axios
        .put(`http://localhost:8080/api/items/${item.model}`, {
          model: this.model,
          part_number: this.part_number,
          project_type: this.project_type,
          quantity: this.quantity,
          priority: this.priority,
          status:this.status,
          startD:this.startD,
          endD:this.endD,
        })
        .then((res) => {
          console.log(res);
          this.getapicall();
          this.putdata = {}
          console.log(res.item.model)
        })
        .catch((err) => {
          console.log("Error : ", err);
        });
      console.log("done");
    }, 
   
 /*  deleteItem: function (index) {
      this.results.splice(index, 1);
      //Can I access item key and tr properties from here?

      // Yes, e.g. to get the text content of the first cell
      const text = this.$refs.rows[index].cells[0].textContent.trim();

      // And add it to the delete button text
      this.$refs.deleteButtons[index].textContent += " " + text;
    }, */
   
    async getapicall() {
      console.log("previous postdata : ", this.postdata);

      await axios
        .get("http://localhost:8080/api/items")
        .then((resp) => {
          this.desserts = resp.data;

          console.log("this.desserts : ", this.desserts);
        })
        .catch((err) => {
          console.log("Error : ", err);
        });
    },
    /* async getapicall2() {
      console.log("previous postdata : ", this.postdata);

      await axios
        .get("http://localhost:8080/api/items")
        .then((resp) => {
          this.desserts = resp.data;

          console.log("this.desserts : ", this.desserts);
        })
        .catch((err) => {
          console.log("Error : ", err);
        });
    }, */

    async save() {
      (this.dialog = false),
        console.log("Updated postdata : ", this.postdata.model);

      await axios
        .post("http://localhost:8080/api/items", this.postdata)
        .then((result) => {
          console.log("Result : ", result);
          this.getapicall();
          this.postdata = {};
          console.log("data inserted : ", this.desserts);
        })
        .catch((err) => {
          console.log("Error : ", err);
        }); 
    },

  /* edit(inputd) {
      this.editdata = inputd[0];
      this.dialog1 = true;
      console.log("input selected : ", this.editdata.id);
      console.log("editdata selected : ", this.editdata);
     
    }, */

  /*  async Edit() {
      this.dialog1 = false;
      console.log("edited data in update : ", this.editdata);

      await axios
        .put(
          "http://localhost:8080/api/items" + this.editdata.id,
          this.editdata
        )
        .then((resp) => {
          console.log(resp);
          this.getapicall();
        })
        .catch((err) => {
          console.log("Error : ", err);
        }); 
     
     
    }, */
  }, 
};
</script>

<style>
.table_border {
  border: 1px solid black;
  background-color: azure;
}

.bAll {
  border: 1px solid black;
}
.bTop {
  border-top: 1px solid black;
}

.bBottom {
  border-bottom: 1px solid black;
}

.bLeft {
  border-left: 1px solid black;
}

.bRight {
  border-right: 1px solid black;
}
.layout {
  padding: 8px 23px;
  width: 10rem;
}
.buttons-me {
  width: 30px;
  margin-left: -10px;
  margin-right: -10px;
}
#edit-form {
  color: black;
  padding-right: 1155px;
  background-color: whitesmoke;
}
#edit-submit {
  color: white;
  background-color: rgb(64, 18, 127);
  margin-bottom: 8px;
}
#edit-card {
  padding-right: 500px;
  color: black;
  background-color: whitesmoke;
}
.edit-lg1 {
}
.edit-lg2 {
  margin-left: 10px;
}
.edit-lg3 {
  margin-left: 50px;
  height: 30px;
}
.edit-submit {
  margin-top: 70px;
  margin-left: 60px;
  margin-bottom: 20px;
}
</style>
