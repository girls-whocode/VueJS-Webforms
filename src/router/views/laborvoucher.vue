<script>
import Layout from '@layouts/main'
import { authMethods } from '@state/helpers'
import appConfig from '@src/app.config'

/* eslint-disable */

export default {
  page: {
    title: 'Labor Vouchers',
    meta: [{ name: 'description', content: appConfig.description }],
  },
  components: { Layout },

  data: function() {
    return {
      fields: [
        { label: 'Type', key: 'voucherType', sortable: 'true' },
        { label: 'Labor Code', key: 'voucherLaborCode', sortable: 'true' },
        { label: 'Labor Hours', key: 'voucherLaborHrs', sortable: 'true' },
        { label: 'Show Details', key: 'voucherDetails' },
      ],
      items: [],
      plLaborCode: null,
      prodLaborCodeOptions: [
        { value: '', text: '' },
        { value: "AFL", text: 'Air Flow'},
        { value: 'PRP', text: 'Airflow Prep Work' },
        { value: 'ASY', text: 'Assembly' },
        { value: 'BRZ', text: 'Braze Assy,Prep,Alloy' },
        { value: 'CHK', text: 'Check (Design)' },
        { value: 'DCL', text: 'Clean - Direct Labor' },
        { value: 'CLN', text: 'Clean / Parts Wash - Indirect' },
        { value: 'DBB', text: 'Debur/Bench' },
        { value: 'DLS', text: 'Develop Laser Setup' },
        { value: 'ECI', text: 'Eddy Current Inspection' },
        { value: 'ECT', text: 'Electrical' },
        { value: 'FAB', text: 'Fabrication' },
        { value: 'DES', text: 'Fixture Design' },
        { value: 'DET', text: 'Fixture Detail' },
        { value: 'HTR', text: 'Heat Treat' },
        { value: 'ISS', text: 'ISS - Waterjet' },
        { value: 'INS', text: 'Inspection/Quality - Direct' },
        { value: 'LAB', text: 'Labs for Quarterly Audit/Process Qualification' },
        { value: 'LAY', text: 'Layout (Design)' },
        { value: 'MPI', text: 'Magnetic Particle Inspection' },
        { value: 'ELC', text: 'Make/Redress Electrodes' },
        { value: 'MAT', text: 'Material Processing' },
        { value: 'RPT', text: 'Penetrant Insp.(FPI) Re-inspection' },
        { value: 'FPI', text: 'Penetrant Inspection(FPI)' },
        { value: 'PGM', text: 'Progamming - 5-ax, CMM, etc. - Direct' },
        { value: 'QLT', text: 'Quality - Indirect' },
        { value: 'REI', text: 'Re-Inspection - Indirect' },
        { value: 'RAD', text: 'Research &amp; Development' },
        { value: 'REV', text: 'Revision (Design)' },
        { value: 'RWK', text: 'Rework' },
        { value: 'SET', text: 'Set Up' },
        { value: 'SHP', text: 'Shipping' },
        { value: 'SFC', text: 'Software/Hardware Ctrl' },
        { value: 'TBB', text: 'Texas Bond and Braze' },
        { value: 'THT', text: 'Texas Heat Treat' },
        { value: 'TPI', text: 'Texas Penetrant Inspection' },
        { value: 'THC', text: 'Through Hole Check' },
        { value: 'TLG', text: 'Tool Assembly' },
        { value: 'TDT', text: 'Tool Detail Fabr.' },
        { value: 'TRN', text: 'Training' },
        { value: 'UTI', text: 'Ultrasonic Inspection' },
        { value: 'WLD', text: 'Welding' },
        { value: 'XRY', text: 'X-Ray/Radiographic Required For Certification' }
      ],
      genLaborCodesOptions: [
        { value: '', text: '' },
        { value: 'BLG', text: 'Building Maintenance' },
        { value: 'CAL', text: 'Calibration' },
        { value: 'CLN', text: 'Clean Prod Parts' },
        { value: 'DBB', text: 'Debur/Bench' },
        { value: 'GNM', text: 'General Maintenance' },
        { value: 'JAN', text: 'Janitorial' },
        { value: 'XAA', text: 'MTT-Administrative Asst.' },
        { value: 'XQ2', text: 'MTT-Contract Review/Job Release' },
        { value: 'XC2', text: 'MTT-Cust Proj - Customer Relations' },
        { value: 'XC3', text: 'MTT-Cust Proj - Engineering Traveler' },
        { value: 'XC4', text: 'MTT-Cust Proj - Filing' },
        { value: 'XC5', text: 'MTT-Cust Proj - Invoicing' },
        { value: 'XC7', text: 'MTT-Cust Proj - Process Development' },
        { value: 'XC8', text: 'MTT-Cust Proj - Quote Support' },
        { value: 'XC9', text: 'MTT-Cust Proj - Quote Support New' },
        { value: 'XC0', text: 'MTT-Cust Proj - Royalties' },
        { value: 'XE1', text: 'MTT-EHS - Development' },
        { value: 'XE2', text: 'MTT-EHS - Project' },
        { value: 'XE3', text: 'MTT-EHS - Support' },
        { value: 'XC1', text: 'MTT-ENG - BOM Tie' },
        { value: 'XN1', text: 'MTT-ENG - Lab Review' },
        { value: 'XN2', text: 'MTT-ENG - NCR support' },
        { value: 'XN3', text: 'MTT-ENG - SPM - Revision or Upgrade' },
        { value: 'XN4', text: 'MTT-ENG - WI - New' },
        { value: 'XN5', text: 'MTT-ENG - WI - Revision or Upgrade' },
        { value: 'XH1', text: 'MTT-HR - Interview' },
        { value: 'XH2', text: 'MTT-HR - Order Supplies' },
        { value: 'XH3', text: 'MTT-HR - Records' },
        { value: 'XH4', text: 'MTT-HR - Testing' },
        { value: 'XH5', text: 'MTT-HR - Time Mgr' },
        { value: 'XQ1', text: 'MTT-QE - Audit' },
        { value: 'XQ3', text: 'MTT-QE - Final Audit' },
        { value: 'XQ4', text: 'MTT-QE - Manual/SPM/Form Revision or Update' },
        { value: 'XQ5', text: 'MTT-QE - NCR support' },
        { value: 'XQ6', text: 'MTT-QE - WI support' },
        { value: 'XQ7', text: 'MTT-QE- Customer Report' },
        { value: 'XQP', text: 'MTT-Quality Project' },
        { value: 'XSS', text: 'MTT-Shop Support' },
        { value: 'XSR', text: 'MTT-Stand-In Receptionist' },
        { value: 'MNG', text: 'Managerial' },
        { value: 'MSC', text: 'Misc.(Meeting,etc.)' },
        { value: 'QLT', text: 'Quality' },
        { value: 'DEV', text: 'Research &amp; Development' },
        { value: 'SOA', text: 'Secr/Office Assist.' },
        { value: 'SHP', text: 'Shipping' },
        { value: 'SFC', text: 'Software/Hardware Ctrl.' },
        { value: 'SUP', text: 'Supervise' },
        { value: 'TLR', text: 'Tool Repair' },
        { value: 'TLG', text: 'Tooling Design / Build / Stock' },
        { value: 'TRN', text: 'Training' },
      ],
      machLaborCodesOptions: [
        { value: '', text: '' },
        { value: 'MAC', text: 'Machine Maintenance' },
        { value: 'TTR', text: 'Titration of Stripping Tank' },
        { value: 'TRN', text: 'Training' },
      ],
      plLaborCode: '',
      plLaborHrs: '',
      plTravlerId: '',
      plOpSeqNum: '',
      plPiecesComplete: '',
      plMachineNum: '',
      plMachineHrs: '',
      glLaborCode: '',
      glGenLaborHrs: '',
      glLaborComments: '',
      mlLaborComments: '',
      mlMachineNum: '',
      mlRequestId: '',
      mlLaborCode: '',
      mlLaborHrs: '',
      sortBy: '',
      sortDesc: '',
    }
  },

  methods: {
    plAdd() {
      const vouchers = {
        voucherType: 'Production',
        voucherLaborCode: this.plLaborCode.toUpperCase(),
        voucherLaborHrs: this.plLaborHrs.toUpperCase(),
        voucherDetails: {
          travlerId: this.plTravlerId.toUpperCase(),
          opSeqNum: this.plOpSeqNum.toUpperCase(),
          piecesComplete: this.plPiecesComplete.toUpperCase(),
          machineNum: this.plMachineNum.toUpperCase(),
          MachineHrs: this.plMachineHrs.toUpperCase(),
        },
      }

      this.items.push(vouchers)
      this.plLaborCode = this.plLaborHrs = this.plTravlerId = this.plOpSeqNum = this.plPiecesComplete = this.plMachineNum = this.plMachineHrs =
        ''
      voucherForm.reset()
    },

    glAdd() {
      const vouchers = {
        voucherType: 'General',
        voucherLaborCode: this.glLaborCode.toUpperCase(),
        voucherLaborHrs: this.glGenLaborHrs.toUpperCase(),
        voucherDetails: { laborComments: this.glLaborComments },
      }

      this.items.push(vouchers)
      this.glLaborCode = this.glGenLaborHrs = this.glLaborComments = ''
      voucherForm.reset()
    },

    mlAdd() {
      const vouchers = {
        voucherType: 'Machine',
        voucherLaborCode: this.mlLaborCode.toUpperCase(),
        voucherLaborHrs: this.mlLaborHrs.toUpperCase(),
        voucherDetails: {
          machineNum: this.mlMachineNum.toUpperCase(),
          requestId: this.mlRequestId.toUpperCase(),
        },
      }

      this.items.push(vouchers)
      this.mlLaborCode = this.mlLaborHrs = this.mlMachineNum = this.mlRequestId =
        ''
      voucherForm.reset()
    },

    removeRow: function(row) {
      this.items.splice(row, 1)
    },

    resetVoucher() {
      this.items = [];
    },

    submitVoucher() {

    },
  },
}
</script>

<template>
  <layout>
    <div id="vouchers" class="container">
      <b-form id="voucherForm" name="voucherForm">
        <div id="pendingVouchers" v-if="items != ''">
            <b-table :sort-by.sync="sortBy" :sort-desc.sync="sortDesc" striped bordered outlined small responsive :items="items" :fields="fields">
              <template>
                <template slot="voucherDetails" slot-scope="row">
                  <b-button variant="primary" size="sm" @click.stop="row.toggleDetails" class="mr-2">
                    {{ row.detailsShowing ? 'Hide' : 'Show'}} Details
                  </b-button>
                  <b-button size="sm" variant="danger" @click="removeRow(row.index)">
                    <font-awesome-icon icon="times" />
                  </b-button>
                </template>
                <template slot="row-details" slot-scope="row">
                  <b-card v-if="row.item.voucherType == 'Production'">
                    <b-row class="mb-2">
                      <b-col sm="3" class="text-sm-right"><b>Travler ID :</b></b-col>
                      <b-col>
                        <span v-if="row.item.voucherDetails.travlerId != ''">{{ row.item.voucherDetails.travlerId }}</span>
                        <span v-else>No Travler ID</span>
                      </b-col>
                      <b-col sm="3" class="text-sm-right"><b>Op Sequence Number :</b></b-col>
                      <b-col>
                        <span v-if="row.item.voucherDetails.opSeqNum != ''">{{ row.item.voucherDetails.opSeqNum }}</span>
                        <span v-else>No Operation Sequence Number</span>
                      </b-col>
                      <b-col sm="3" class="text-sm-right"></b-col>
                      <b-col></b-col>
                    </b-row>
                    <b-row class="mb-2">
                      <b-col sm="3" class="text-sm-right"><b>Pieces Completed :</b></b-col>
                      <b-col>
                        <span v-if="row.item.voucherDetails.piecesComplete != ''">{{ row.item.voucherDetails.piecesComplete }}</span>
                        <span v-else>0</span>
                      </b-col>
                      <b-col sm="3" class="text-sm-right">
                        <b>Machine Number :</b>
                      </b-col>
                      <b-col>
                        <span v-if="row.item.voucherDetails.machineNum != ''">{{ row.item.voucherDetails.machineNum }}</span>
                        <span v-else>No Machine Number</span>
                      </b-col>
                      <b-col sm="3" class="text-sm-right"><b>Machine Hours :</b></b-col>
                      <b-col>
                        <span v-if="row.item.voucherDetails.MachineHrs != ''">{{ row.item.voucherDetails.MachineHrs }}</span>
                        <span v-else>No Machine Hours</span>
                      </b-col>
                    </b-row>
                  </b-card>
                  <b-card v-if="row.item.voucherType == 'General'">
                    <b-row class="mb-2">
                      <b-col class="text-sm">
                        <b>Comments :</b>
                      </b-col>
                    </b-row>
                    <b-row class="mb-2">
                      <b-col style="text-align: justify;">
                        <span v-if="row.item.voucherDetails.laborComments != ''">{{ row.item.voucherDetails.laborComments }}</span>
                        <span v-else>No Comment</span>
                      </b-col>
                    </b-row>
                  </b-card>
                  <b-card v-if="row.item.voucherType == 'Machine'">
                    <b-row class="mb-2">
                      <b-col sm="3" class="text-sm-right"><b>Machine Number :</b></b-col>
                      <b-col>
                        <span v-if="row.item.voucherDetails.machineNum != ''">{{ row.item.voucherDetails.machineNum }}</span>
                        <span v-else>No Machine Number</span>
                      </b-col>
                      <b-col sm="3" class="text-sm-right">
                        <b>Request ID :</b>
                      </b-col>
                      <b-col>
                        <span v-if="row.item.voucherDetails.requestId != ''">{{ row.item.voucherDetails.requestId }}</span>
                        <span v-else>No Request ID</span>
                      </b-col>
                    </b-row>
                  </b-card>
                </template>
              </template>
            </b-table>
          <b-row>
            <b-col sm="6">
              <b-button-group class="button-sm float-left">
                <b-button variant="danger" @click="resetVoucher">Reset Voucher</b-button>
              </b-button-group>
            </b-col>
            <b-col sm="6">
              <b-button-group class="button-sm float-right">
                <b-button variant="primary" @click="submitVoucher">Approve and Submit Voucher</b-button>
              </b-button-group>
            </b-col>
          </b-row>
        </div>
        <div id="productionLabor">
          <b-card-group deck class="user-forms">
            <b-card header="Production Labor Voucher" header-tag="header">
              <b-container>
                <b-row>
                  <b-col sm="2">
                    <div class="form-label-group">
                      <input id="plTravlerId" v-model="plTravlerId" type="text" name="plTravlerId" class="form-control text-uppercase" placeholder="Travler ID">
                      <label for="plTravlerId">Travler ID</label>
                    </div>
                  </b-col>
                  <b-col sm="2">
                    <div class="form-label-group">
                      <input type="text" id="plOpSeqNum" name="plOpSeqNum" v-model="plOpSeqNum" class="form-control text-uppercase" placeholder="Op Sequence #">
                      <label for="plOpSeqNum">Op Sequence #</label>
                    </div>
                  </b-col>
                  <b-col sm="6">
                    <div class="form-label-group">
                      <b-form-select id="plLaborCode" v-model="plLaborCode" :options="prodLaborCodeOptions" class="mb-3" required></b-form-select>
                      <label for="plLaborCode">Labor Code</label>
                    </div>
                  </b-col>
                  <b-col sm="2">
                    <div class="form-label-group">
                      <input type="text" id="plLaborHrs" name="plLaborHrs" v-model="plLaborHrs" class="form-control text-uppercase" placeholder="Labor Hours">
                      <label for="plLaborHrs">Labor Hours</label>
                    </div>
                  </b-col>
                </b-row>
                <b-row>
                <b-col sm="2">
                  <div class="form-label-group">
                    <input type="text" id="plPiecesComplete" name="plPiecesComplete" v-model="plPiecesComplete" class="form-control text-uppercase" placeholder="Pieces Complete">
                    <label for="plPiecesComplete">Pieces Complete</label>
                  </div>
                </b-col>
                <b-col sm="2">
                  <div class="form-label-group">
                    <input type="text" id="plMachineNum" name="plMachineNum" v-model="plMachineNum" class="form-control text-uppercase" placeholder="Machine Number">
                    <label for="plMachineNum">Machine Number</label>
                  </div>
                </b-col>
                <b-col sm="2">
                  <div class="form-label-group">
                    <input type="text" id="plMachineHrs" name="plMachineHrs" v-model="plMachineHrs" class="form-control text-uppercase" placeholder="Machine Hours">
                    <label for="plMachineHrs">Machine Hours</label>
                  </div>
                </b-col>
                <b-col sm="6">
                  <b-button-group class="button-sm float-right">
                    <b-button variant="success" @click="plAdd">Add to Voucher</b-button>
                  </b-button-group>
                </b-col>
              </b-row>
            </b-container>
          </b-card>
        </b-card-group>
      </div>
        <div id="generalLabor">
          <b-card-group deck class="user-forms">
            <b-card header="General Labor Voucher" header-tag="header">
              <b-container>
                <b-row>
                    <b-col sm="10">
                      <div class="form-label-group">
                        <b-form-select id="glLaborCode" v-model="glLaborCode" :options="genLaborCodesOptions" class="mb-3" required></b-form-select>
                        <label for="glLaborCode">Labor Code</label>
                      </div>
                    </b-col>
                    <b-col sm="2">
                      <div class="form-label-group">
                        <input type="text" id="glGenLaborHrs" name="glGenLaborHrs" v-model="glGenLaborHrs" class="form-control text-uppercase" placeholder="Labor Hours">
                        <label for="glGenLaborHrs">Labor Hours</label>
                      </div>
                    </b-col>
                  </b-row>
                <b-row>
                    <b-col sm="10">
                      <div class="form-label-group">
                        <textarea class="form-control" id="glLaborComments" name="glLaborComments" v-model="glLaborComments" placeholder="Comments" rows="3"></textarea>
                        <label for="glLaborComments">Comments</label>
                      </div>
                    </b-col>
                    <b-col sm="2">
                      <b-button-group class="button-sm float-right">
                        <b-button variant="success" @click="glAdd">Add to Voucher</b-button>
                      </b-button-group>
                    </b-col>
                  </b-row>
              </b-container>
            </b-card>
          </b-card-group>
        </div>
        <div id="machineLabor">
          <b-card-group deck class="user-forms">
            <b-card header="Machine Maintenance Voucher" header-tag="header">
              <b-container>
                <b-row>
                  <b-col sm="2">
                    <div class="form-label-group">
                      <input type="text" id="mlMachineNum" name="mlMachineNum" v-model="mlMachineNum" class="form-control text-uppercase" placeholder="Machine Number">
                      <label for="mlMachineNum">Machine Number</label>
                    </div>
                  </b-col>
                  <b-col sm="6">
                    <div class="form-label-group">
                      <b-form-select id="mlLaborCode" v-model="mlLaborCode" :options="machLaborCodesOptions" class="mb-3" required></b-form-select>
                      <label for="mlLaborCode">Labor Code</label>
                    </div>
                  </b-col>
                  <b-col sm="2">
                    <div class="form-label-group">
                      <input type="text" id="mlLaborHrs" name="mlLaborHrs" v-model="mlLaborHrs" class="form-control text-uppercase" placeholder="Labor Hours">
                      <label for="mlLaborHrs">Labor Hours</label>
                    </div>
                  </b-col>
                  <b-col sm="2">
                    <div class="form-label-group">
                      <input type="text" id="mlRequestId" name="mlRequestId" v-model="mlRequestId" class="form-control text-uppercase" placeholder="Request ID">
                      <label for="mlRequestId">Request ID</label>
                    </div>
                  </b-col>
                </b-row>
                <b-row>
                  <b-col sm="12">
                      <b-button-group class="button-sm float-right">
                        <b-button variant="success" @click="mlAdd">Add to Voucher</b-button>
                      </b-button-group>
                  </b-col>
                </b-row>
              </b-container>
            </b-card>
          </b-card-group>
        </div>
      </b-form>
    </div>
  </layout>
</template>

<style lang="scss">
@import '@design';

.container {
  min-width: $size-content-width-min;
  max-width: $size-content-width-max/2;
  margin: 0 auto;
}

#vouchers {
  margin-top: 60px;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

:root {
  --input-padding-x: 0.5rem;
  --input-padding-y: 0.5rem;
}
</style>
