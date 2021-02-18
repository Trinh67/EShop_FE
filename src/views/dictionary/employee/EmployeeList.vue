<template>
  <div class="content-body">
    <div class="header-content">
      <div class="title">Danh sách nhân viên</div>
      <div class="content-feature">
        <button
          id="btnAdd"
          class="m-btn m-btn-default"
          v-on:click="btnAddOnClick"
        >
          <div class="m-btn-icon icon-add"></div>
          <div class="btn-text">Thêm nhân viên</div>
        </button>
        <Details @closePopup="closePopup" :isHide="isHideParent"/>
      </div>
    </div>
    <div class="filter-bar">
      <div class="filter-left">
        <input
          id="txtSearchEmployee"
          class="icon-search input-search"
          type="text"
          placeholder="Tìm kiếm theo Mã, Tên hoặc Số điện thoại"
        />
        <select
          id="cbxDepartment"
          fieldName="CustomerGroupName"
          fieldValue="CustomerGroupId"
          api="/api/customergroups"
          class="m-control"
        >
          <option value="19165ed7-212e-21c4-0428-030d4265475f">
            Tất cả phòng ban
          </option>
          <option class="" value="148ed882-32b8-218e-9c20-39c2f00615e8">Phòng nhân sự</option>
          <option class="" value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">Phòng quản lý</option>
          <option class="" value="3700cc49-55b5-69ea-4929-a2925c0f334d">Phòng đào tạo</option>
        </select>
        <select
          id="cbxPosition"
          fieldName="CustomerGroupName"
          fieldValue="CustomerGroupId"
          api="/api/customergroups"
          class="m-control"
        >
          <option value="19165ed7-212e-21c4-0428-030d4265475f">
            Tất cả vị trí
          </option>
          <option value="19165ed7-212e-21c4-0428-030d4265475f">Giám đốc</option>
          <option value="7a0b757e-41eb-4df6-c6f8-494a84b910f4">
            Trưởng phòng
          </option>
          <option value="3631011e-4559-4ad8-b0ad-cb989f2177da">
            Nhân viên
          </option>
        </select>
      </div>
      <div class="filter-right">
        <button id="btnRefresh" class="m-second-button m-btn-refresh"></button>
      </div>
    </div>
    
    <div
      class="grid grid-employee el-table el-table--fit el-table--scrollable-y el-table--enable-row-hover el-table--enable-row-transition"
    >
      <table
        id="tbListData"
        cellspacing="0"
        cellpadding="0"
        border="0"
        class="el-table__body"
        style="min-width: 100%"
      >
        <thead class="has-gutter">
          <tr class="el-table__row">
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_114 is-leaf"
              fieldName="EmployeeCode"
            >
              <div class="cell">Mã nhân viên</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_115 is-leaf"
              fieldName="FullName"
            >
              <div class="cell">Họ và tên</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="GenderName"
            >
              <div class="cell">Giới tính</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="DateOfBirth"
              formatType="ddmmyyyy"
              style="text-align: center"
            >
              <div class="cell">Ngày sinh</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="PhoneNumber"
            >
              <div class="cell">Điện thoại</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="Email"
            >
              <div class="cell">Email</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="PositionName"
            >
              <div class="cell">Chức vụ</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="DepartmentName"
            >
              <div class="cell">Phòng ban</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="Salary"
              formatType="Money"
            >
              <div class="cell" style="text-align: right">Mức lương cơ bản</div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              class="el-table_30_column_116 is-leaf"
              fieldName="WorkStatusName"
            >
              <div class="cell">Tình trạng công việc</div>
            </th>
            <th class="gutter" style="width: 4px"></th>
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
              <div class="cell">{{ employee.EmployeeCode }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.FullName }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.GenderName }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.DateOfBirth }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.PhoneNumber }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.Email }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.PositionName }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.DepartmentName }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.Salary }}</div>
            </td>
            <td>
              <div class="cell">{{ employee.WorkStatusName }}</div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <div class="paging-bar">
      <div class="paging-record-info">Hiển thị <b>{{startListEmp}}-{{finishListEmp}}/{{empDataLength}}</b> nhân viên</div>
      <div class="paging-option">
        <div class="btn-select-page m-btn-firstpage"></div>
        <div class="btn-select-page m-btn-prev-page"></div>
        <div class="m-btn-list-page">
          <button class="btn-pagenumber btn-pagenumber-selected">1</button>
          <button class="btn-pagenumber">2</button>
          <button class="btn-pagenumber">3</button>
          <button class="btn-pagenumber">4</button>
        </div>
        <div class="btn-select-page m-btn-next-page"></div>
        <div class="btn-select-page m-btn-lastpage"></div>
      </div>
      <div class="paging-record-option">
        <select v-model="number">
          <option :value='10'>10 nhân viên/trang</option>
          <option :value='15'>15 nhân viên/trang</option>
          <option :value='25'>25 nhân viên/trang</option>
          <option :value='50'>50 nhân viên/trang</option>
        </select>
      </div>
    </div>
    
  </div>
</template>

<script src="https://unpkg.com/vue"></script>
<script>
import Vue from 'vue';
import * as axios from "axios";
import Details from "./EmployeeProfileDetail";
export default {
  name: "Employees",
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
      number: 10,
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
          text: "Mã nhân viên",
          align: "start",
          sortable: false,
          value: "EmployeeCode",
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
        .get('https://localhost:44337/api/Employees/' + this.startPoint*this.number + '/' + this.number)
        //.get('https://localhost:44337/api/Employees')
        .then(response => {
            this.employees = response.data['Data'];
            //this.EmpDataLength = response.data['Data'].length;
            this.startListEmp = this.number*this.startPoint + 1;
            this.finishListEmp = this.number*(this.startPoint + 1);
            this.startListEmp = this.number*this.startPoint + 1;
            this.finishListEmp = this.number*(this.startPoint + 1);
            formEmpData(this.employees);
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
    const response = await axios.get("https://localhost:44337/api/Employees");
    this.employees = response.data['Data'].slice(this.startPoint, this.number);
    this.empDataLength = response.data['Data'].length;
    this.startListEmp = this.number*this.startPoint + 1;
    this.finishListEmp = this.number*(this.startPoint + 1);
    formEmpData(this.employees);
  },
};

/**
 * Tạo dữ liệu mẫu
 */
var day, month, year;
var gender = ["Nữ", "Nam", "Khác"];
var positionList = {'2b031b59-5276-589c-9d75-2a7ae1c799c4': '', '26021185-77af-263c-842a-acc8fc2f00af': 'Trưởng phòng', '2b031b59-5276-589c-9d75-2a7ae1c799c8': 'Nhân viên', '6118a7ff-742b-25db-a9c1-8e252c39bb73': 'Giám đốc' };
var departmentList = { '25c6c36e-1668-7d10-6e09-bf1378b8dc98': '', '148ed882-32b8-218e-9c20-39c2f00615e8': 'Phòng nhân sự', '25c6c36e-1668-7d10-6e09-bf1378b8dc91': 'Phòng quản lý', '3700cc49-55b5-69ea-4929-a2925c0f334d': 'Phòng đào tạo' };
var statusList = ["Đã nghỉ việc", "Đang thử việc", "Đang làm việc", "Đã nghỉ hưu"];

/**
 * Format Number
 */
// var numeral = require("numeral");
// Vue.filter("formatNumber", function (value) {
//     return numeral(value).format("0,0");
// });

/**
 * Format Employees Data
 */
function formEmpData(emp){
    for (var i = 0; i < emp.length; i++) {
        emp[i]['isChecked'] == false;
        if (emp[i]['Gender'] == null) emp[i]['Gender'] = ""; else emp[i]['Gender'] = gender[emp[i]['Gender']];
        if (emp[i]['DateOfBirth'] == null) emp[i]['DateOfBirth'] = ""; else emp[i]['DateOfBirth'] = formDate(emp[i]['DateOfBirth']);
        if (emp[i]['Email'] == null) emp[i]['Email'] = "";
        if (emp[i]['PositionId'] == null) emp[i]['PositionId'] = ""; else emp[i]['PositionId'] = positionList[emp[i]['PositionId']];
        if (emp[i]['DepartmentId'] == null) emp[i]['DepartmentId'] = ""; else emp[i]['DepartmentId'] = departmentList[emp[i]['DepartmentId']];
        if (emp[i]['Salary'] == null) emp[i]['Salary'] = "";
        if (emp[i]['Status'] == null) emp[i]['Status'] = ""; else emp[i]['Status'] = statusList[emp[i]['Status']];
    }
}

/**
 * Format Date
 */
function formDate(dateValue) {
    let date = new Date(dateValue);
    day = date.getDate();
    month = date.getMonth() + 1;
    year = date.getFullYear();
    return day + '/' + month + '/' + year;
}
</script>

<style scoped>
.grid-employee {
  margin-top: 10px;
  height: calc(100vh - 234px);
}

.el-avatar-employee {
  padding-top: 16px;
  padding-right: 16px;
}

.el-left {
  width: calc(100% - 180px);
}

.el-avatar-employee .el-avatar {
  border: 1px solid #ccc;
  width: 160px;
  height: 160px;
  margin: 0 auto;
  border-radius: 50%;
  cursor: pointer;
  /* background-image: url("/assets/img/default-avatar.jpg"); */
  background-repeat: no-repeat;
  background-position: center;
  background-size: cover;
}

.el-avatar-note {
  font-size: 12px;
}
.filter-left {
  display: flex;
}
.filter-left select {
  margin-left: 10px;
  margin-right: 10px;
}

.currency-for-input {
  position: absolute;
  right: 40px;
  line-height: 40px;
  font-style: italic;
}

#txtSearchEmployee {
  min-width: 300px;
}
</style>