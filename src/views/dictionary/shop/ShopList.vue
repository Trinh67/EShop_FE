<template>
  <div class="content-body">
    <div class="header-content">
      <div class="toolbar">
        <button class="m-btn m-btn-default" v-on:click="btnAddOnClick">
          <div class="btn-toolbar-icon icon-add"></div> Thêm mới
        </button>
        <button class="m-btn m-btn-default"><div class="btn-toolbar-icon icon-multiply"></div> Nhân bản</button>
        <button class="m-btn m-btn-default"><div class="btn-toolbar-icon icon-edit"></div> Sửa </button>
        <button class="m-btn m-btn-default"><div class="btn-toolbar-icon icon-delete"></div> Xóa </button>
        <button class="m-btn m-btn-default"><div class="btn-toolbar-icon icon-load"></div> Nạp </button>
        <Details @closePopup="closePopup" :isHide="isHideParent"/>
      </div>
      <!-- <div class="content-feature">
        <button
          id="btnAdd"
          class="m-btn m-btn-default"
          v-on:click="btnAddOnClick"
        >
          <div class="m-btn-icon icon-add"></div>
          <div class="btn-text">Thêm nhân viên</div>
        </button>
        <Details @closePopup="closePopup" :isHide="isHideParent"/>
      </div> -->
    </div> 
    <div
      class="grid grid-shop el-table el-table--fit el-table--scrollable-y el-table--enable-row-hover el-table--enable-row-transition"
    >
      <table
        id="tbListData"
        cellspacing="0"
        cellpadding="0"
        style="min-width: 100%"
      >
        <thead>
          <tr class="el-table__row">
            <th
              colspan="1"
              rowspan="1"
              width=12%
              class="el-table_30_column_114 is-leaf"
              fieldName="ShopCode"
            >
              <div class="cell">Mã cửa hàng</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              width=20%
              class="el-table_30_column_116 is-leaf"
              fieldName="ShopName"
            >
              <div class="cell">Tên cửa hàng</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              width=44%
              class="el-table_30_column_115 is-leaf"
              fieldName="Address"
            >
              <div class="cell">Địa chỉ</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              width=12%
              class="el-table_30_column_116 is-leaf"
              fieldName="PhoneNumber"
            >
              <div class="cell">Số điện thoại</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              width=12%
              class="el-table_30_column_116 is-leaf"
              fieldName="StatusName"
            >
              <div class="cell">Trạng thái</div>
            </th>
          </tr>
          <tr>
            <th>
              <select class="select-filter-button">
                <option>* : Chứa</option>
                <option>= : Bằng</option>
                <option>+ : Bắt đầu bằng</option>
                <option>- : Kết thúc bằng</option>
                <option>! : Không chứa</option>
              </select>
              <input
                id="txtSearchShopCode"
                class="input-search"
                type="text"
                placeholder=""
              />
            </th>
            <th>
              <select class="select-filter-button">
                <option value="*">* : Chứa</option>
                <option value="=">= : Bằng</option>
                <option value="+">+ : Bắt đầu bằng</option>
                <option value="-">- : Kết thúc bằng</option>
                <option value="!">! : Không chứa</option>
              </select>
              <input
                id="txtSearchShopName"
                class="input-search"
                type="text"
                placeholder=""
              />
            </th>
            <th>
              <select class="select-filter-button">
                <option>* : Chứa</option>
                <option>= : Bằng</option>
                <option>+ : Bắt đầu bằng</option>
                <option>- : Kết thúc bằng</option>
                <option>! : Không chứa</option>
              </select>
              <input
                id="txtSearchAddress"
                class="input-search"
                type="text"
                placeholder=""
              />
            </th>
            <th>
              <select class="select-filter-button">
                <option>* : Chứa</option>
                <option>= : Bằng</option>
                <option>+ : Bắt đầu bằng</option>
                <option>- : Kết thúc bằng</option>
                <option>! : Không chứa</option>
              </select>
              <input
                id="txtSearchPhoneNumber"
                class="input-search"
                type="text"
                placeholder=""
              />
            </th>
            <th>
              <select
                id="txtSearchStatus"
                fieldName="StatusName"
                fieldValue="StatusId"
                api="/api/customergroups"
                class="m-control"
              >
                <option value="">
                  Tất cả trạng thái
                </option>
                <option class="" value="148ed882-32b8-218e-9c20-39c2f00615e8">Đang hoạt động</option>
                <option class="" value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">Tạm dừng hoạt động</option>
                <option class="" value="3700cc49-55b5-69ea-4929-a2925c0f334d">Chờ kích hoạt</option>
              </select>
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            class="el-table__row"
            v-for="employee in employees"
            :key="employee.EmployeeId"
            @dblclick="rowOnClick(employee)"
          >
            <td>
              <div>{{ employee.shopCode }}</div>
            </td>
            <td>
              <div>{{ employee.shopName }}</div>
            </td>
            <td>
              <div>{{ employee.address }}</div>
            </td>
            <td>
              <div>{{ employee.phoneNumber }}</div>
            </td>
            <td>
              <div>{{ employee.statusName }}</div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="paging-bar">
      <div class="paging-option">
        <div class="btn-select-page m-btn-firstpage"></div>
        <div class="btn-select-page m-btn-prev-page"></div>
        <div class="m-btn-list-page">
          Trang
          <button class="btn-pagenumber btn-pagenumber-selected">1</button>
          trên {{totalPage}}
        </div>
        <div class="btn-select-page m-btn-next-page"></div>
        <div class="btn-select-page m-btn-lastpage"></div>
        <div class="btn-select-page m-btn-refresh"></div>
      </div>
      <div class="paging-record-option">
        <select v-model="number" class="input-number-record">
          <option :value='15'>15 </option>
          <option :value='25'>25 </option>
          <option :value='50'>50 </option>
          <option :value='100'>100 </option>
        </select>
      </div>
      <div class="paging-record-info">Hiển thị <b>{{startListEmp}}-{{finishListEmp}}/{{empDataLength}}</b> nhân viên</div>
    </div>
    
  </div>
</template>

<script src="https://unpkg.com/vue"></script>
<script>
import Vue from 'vue';
import * as axios from "axios";
import Details from "./ShopProfileDetail";
export default {
  name: "Shop",
  components: {
    Details,
  },

  data() {
    return {
      isHideParent: true,
      // Dữ liệu tìm kiếm
      empCode: null,
      position: "no",
      department: "no",
      // Phân trang
      empDataLength: 800,
      startPoint: 0,
      number: 15,
      totalPage: 10,
      startListEmp: 1,
      finishListEmp: 1,

      /**
       * Dữ liệu nhân viên
       */
      selectedEmployee: {
        EmployeeId: 1,
        FullName: "Nguyễn Văn Mạnh",
      },
      employees: [],
      headers: [
        {
          text: "Mã cửa hàng",
          align: "start",
          sortable: false,
          value: "ShopCode",
        },
        { text: "Họ và tên", value: "FullName", align: "end" },
        { text: "Ngày sinh", value: "DateOfBirth" },
        { text: "Giới tính", value: "GenderName" },
        { text: "Vị trí", value: "PositionName" },
        { text: "Phòng ban", value: "DepartmentName" },
        { text: "Địa chỉ Email", value: "Email" },
        { text: "Số điện thoại", value: "PhoneNumber" },
        { text: "Mức lương", value: "Salary" },
        { text: "Địa chỉ", value: "Address" },
        { text: "Trạng thái công việc", value: "WorkStatusName" },
      ],
    };
  },

  methods: {
    btnAddOnClick() {
      this.isHideParent = false;
    },
    rowOnClick(employee){
      alert(employee.FullName);
    },
    closePopup(isHide){
      this.isHideParent = isHide;
    },
    /**
     * Load dữ liệu theo điểm đầu và số lượng bản ghi
     */
    loadData(){
        axios
        .get('http://localhost:52698/api/v1/shops/GetWithRange?startPoint=' + this.startPoint*this.number + '&number=' + this.number)
        .then(response => {
            this.employees = response.data;
            this.startListEmp = this.number*this.startPoint + 1;
            this.finishListEmp = this.number*(this.startPoint + 1);
            this.totalPage = Math.ceil(this.empDataLength/this.number);
        })
        .catch(error => {
            console.log(error)
            this.errored = true
        })
        .finally(() => this.loading = false);
    },
  },
  /**
   * Theo dõi thay đổi của biến 
   */
  watch: {
        number: function() {
            this.loadData();
        }
    },
  async created() {
    const response = await axios.get("http://localhost:52698/api/v1/shops");
    this.employees = response.data.slice(this.startPoint, this.number);
    this.empDataLength = response.data.length;
    this.startListEmp = this.number*this.startPoint + 1;
    this.finishListEmp = this.number*(this.startPoint + 1);
    this.totalPage = Math.ceil(this.empDataLength/this.number);
  },
};
</script>

<style scoped>
.grid-shop {
  height: calc(100vh - 180px);
}

tr .filter{
  height: 40px;
}

.currency-for-input {
  position: absolute;
  right: 40px;
  line-height: 40px;
  font-style: italic;
}

.select-filter-button{
  align-items: center;
  width: 40px;
  height: 40px;
  font-size: 13px;
  color: #000000;
  font-family: GoogleSans-Regular;
  padding-left: 16px;
  padding-right: 16px;
  margin: 4px;
  outline: none;
  border: 1px solid #d9d9d9 !important;
  cursor: pointer;
  justify-content: center;
}
#txtSearchShopCode, #txtSearchShopName, #txtSearchAddress, #txtSearchPhoneNumber{
  min-width: calc(100% - 52px);
  border: 1px solid #d9d9d9 !important;
}
#txtSearchStatus{
  margin: 4px;
  border: 1px solid #d9d9d9 !important;
  width: calc(100% - 8px);
}
td.filter{
  padding: 0px !important;
}
select.input-number-record{
  min-width: 30px;
}
</style>