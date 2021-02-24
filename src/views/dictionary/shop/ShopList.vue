<template>
  
  <div class="content-body">
    <!-- Loading -->
    <div class="vld-parent">
        <loading :active.sync="isLoading" 
        :can-cancel="false" 
        @click="onCancel"
        :is-full-page="fullPage"></loading>
    </div>
    <!-- Content Header -->
    <div class="header-content">
      <div class="toolbar">
        <button 
          class="m-btn m-btn-default" 
          @click="btnAddOnClick"
        >
          <div class="btn-toolbar-icon icon-add"></div> Thêm mới
        </button>
        <button class="m-btn m-btn-default" disabled id="duplicate">
          <div class="btn-toolbar-icon icon-multiply"></div> Nhân bản
        </button>
        <button 
          class="m-btn m-btn-default"
          @click="btnEditOnClick"
        >
          <div class="btn-toolbar-icon icon-edit"></div> Sửa 
        </button>
        <button 
          class="m-btn m-btn-default" 
          @click="btnDeleteOnClick">
          <div class="btn-toolbar-icon icon-delete"></div> Xóa 
        </button>
        <button class="m-btn m-btn-default"><div class="btn-toolbar-icon icon-load" @click="reloadData"></div> Nạp </button>
        <Details @closePopup="closePopup" :isHide="isHideParent" :titleDialog="title" @reload="reloadData"/>
        <DialogDel @closeDelDialog="closePopup" :isHideDelDialog="isHideDel" :titleDelDialog="title" :shopId="selectedId" :shopName="shopNameSelected" @reload="reloadData"/>
      </div>
    </div> 
    <!-- Content Body -->
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
            >
              <div class="cell">Mã cửa hàng<br/></div>
              <div class="group-input">
                <input class="select-filter-button" placeholder="*" disabled/>
                <input
                  id="txtSearchShopCode"
                  class="input-search"
                  type="text"
                  placeholder=""
                  v-model="txtSearchShopCode"
                  @change="SearchShop()"
                />
              </div>
              
            </th>
            <th
              colspan="1"
              rowspan="1"
              width=20%
              class="el-table_30_column_116 is-leaf"
            >
              <div class="cell">Tên cửa hàng<br/></div>
              <div class="group-input">
                <input class="select-filter-button" placeholder="*" disabled/>
                <input
                  id="txtSearchShopName"
                  class="input-search"
                  type="text"
                  placeholder=""
                  v-model="txtSearchShopName"
                  @change="SearchShop()"
                />
              </div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              width=44%
              class="el-table_30_column_115 is-leaf"
            >
              <div class="cell">Địa chỉ<br/></div>
              <div class="group-input">
                <input class="select-filter-button" placeholder="*" disabled/>
                <input
                  id="txtSearchAddress"
                  class="input-search"
                  type="text"
                  placeholder=""
                  v-model="txtSearchAddress"
                  @change="SearchShop()"
                />
              </div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              width=12%
              class="el-table_30_column_116 is-leaf"
            >
              <div class="cell">Số điện thoại<br/></div>
              <div class="group-input">
                <input class="select-filter-button" placeholder="*" disabled/>
                <input
                  id="txtSearchPhoneNumber"
                  class="input-search"
                  type="text"
                  placeholder=""
                  v-model="txtSearchPhoneNumber"
                  @change="SearchShop()"
                />
              </div>
            </th>
            <th
              colspan="1"
              rowspan="1"
              width=12%
              class="el-table_30_column_116 is-leaf"
            >
              <div class="cell">Trạng thái<br/></div>
              <div class="group-input">
                <select
                  id="txtSearchStatus"
                  class="m-control"
                  v-model="txtSearchStatus"
                  @change="SearchShop()"
                >
                  <option value="">
                    Tất cả trạng thái
                  </option>
                  <option class="" value="674934cc-42cf-20cf-1d4a-aea48a10ed18">Đang hoạt động</option>
                  <option class="" value="64a59a25-2488-54b0-f6b4-c8af08a50cbf">Tạm dừng hoạt động</option>
                  <option class="" value="34bd2cef-5026-567c-3b71-153b37881afe">Chờ kích hoạt</option>
                </select>
              </div>
            </th>
          </tr>
        </thead>
        <tbody id="tbody">
          <tr
            class="el-table__row"
            v-for="shop in shops"
            :key="shop.shopId"
            :id="shop.shopId"
            @click="rowOnClick(shop.shopId, shop.shopName)"
            @dblclick="rowOnDBClick(shop.shopId)"
          >
            <td>
              <div>{{ shop.shopCode }}</div>
            </td>
            <td>
              <div>{{ shop.shopName }}</div>
            </td>
            <td>
              <div>{{ shop.address }}</div>
            </td>
            <td>
              <div>{{ shop.phoneNumber }}</div>
            </td>
            <td>
              <div>{{ shop.statusName }}</div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    <!-- Content footer -->
    <div class="paging-bar">
      <div class="paging-option">
        <div class="btn-select-page m-btn-firstpage" v-on:click="FirstPageNumber"></div>
        <div class="btn-select-page m-btn-prev-page" v-on:click="DecreasePageNumber"></div>
        <div class="m-btn-list-page">
          Trang
          <input 
            type="number" 
            v-model="currentPage"
            id="current-page"
            @change="SetCurrentPage()"
          />
          trên {{totalPage}}
        </div>
        <div class="btn-select-page m-btn-next-page" v-on:click="IncreasePageNumber"></div>
        <div class="btn-select-page m-btn-lastpage" v-on:click="LastPageNumber"></div>
        <div class="btn-select-page m-btn-refresh" @click="reloadData"></div>
      </div>
      <div class="paging-record-option">
        <select v-model="number" class="input-number-record">
          <option :value='15'>15 </option>
          <option :value='25'>25 </option>
          <option :value='50'>50 </option>
          <option :value='100'>100 </option>
        </select>
      </div>
      <div class="paging-record-info">Hiển thị <b>{{startListShop}}-{{finishListShop}}/{{shopDataLength}}</b> nhân viên</div>
    </div>
  </div>
</template>

<script src="https://unpkg.com/vue"></script>
<script>
import Vue from 'vue';
import * as axios from "axios";
import Details from "./ShopProfileDetail";
import DialogDel from "@/components/base/TheDialogDel"
import { EventBus } from '@/EventBus.js'
// Import component
import Loading from 'vue-loading-overlay';
// Import stylesheet
import 'vue-loading-overlay/dist/vue-loading.css';
import '@/styles/pages/shopList.scss';
export default {
  name: "Shop",
  components: {
    Details,
    DialogDel,
    Loading,
  },

  data() {
    return {
      /**
       * Loading popup
       * Created By: TXTrinh (23/02/2021)
       */
      isLoading: false,
      fullPage: true,
      
      isHideParent: true,
      isHideDel: true,
      shopNameSelected: "",
      selectedId: null,
      title: "",
      /**
       * Dữ liệu dùng để tìm kiếm
       * Create By: TXTrinh (22/02/2021)
       */
      txtSearchShopCode: "",
      txtSearchShopName: "",
      txtSearchAddress: "",
      txtSearchPhoneNumber: "",
      txtSearchStatus: "",
      
      /**
       * Dữ liệu dùng phân trang
       * Create By: TXTrinh (22/02/2021)
       */
      shopDataLength: 200,
      startPoint: 0,
      number: 15,
      totalPage: 10,
      startListShop: 1,
      finishListShop: 1,
      currentPage: 1,
      /**
       * Dữ liệu thông tin cửa hàng
       * Create By: TXTrinh (22/02/2021)
       */
      shops: [],
      
    };
  },

  methods: {
    /**
     * Thoát Loading
     */
    onCancel() {
      console.log('User cancelled the loader.');
    },
    /**
     * Hàm sử lí sự kiện nhấn vào thêm mới
     * Create By: TXTrinh (22/02/2021)
     */
    btnAddOnClick() {
      this.isHideParent = false;
      this.title = "Thêm mới cửa hàng";
      EventBus.$emit('addShop', this.isHideParent);
    },
    /**
     * Hàm sử lí sự kiện nhấn vào sửa
     * Created By: TXTrinh (22/02/2021)
     */
    btnEditOnClick(){
      if(this.selectedId == null || this.selectedId == "") return;
      this.isHideParent = false;
      this.title = "Cập nhập cửa hàng";
      EventBus.$emit('showShop', this.selectedId);
    },
    /**
     * Hàm sử lí sự kiện nhấn vào Xóa
     * Created By: TXTrinh (22/02/2021)
     */
    btnDeleteOnClick(){
      if(this.selectedId == null || this.selectedId == "") return;
      this.isHideDel = false;
      this.title = "Xóa dữ liệu";
    },
    /**
     * Load lại dữ liệu
     * Create By: TXTrinh (22/02/2021)
     */
    reloadData(){
      this.$emit('reloadData');
    },
    /**
     * Sự kiện click vào 1 hàng
     * Created By: TXTrinh (22/02/2021)
     */
    rowOnClick(id, name){
      if(this.selectedId == id){
       document.getElementById(id).classList.remove("selected");
       this.selectedId = null;
      }
      else if(this.selectedId != null && this.selectedId!= ""){
        document.getElementById(this.selectedId).classList.remove("selected");
        document.getElementById(id).classList.add("selected");
        this.selectedId = id;
        this.shopNameSelected = name;
      } else{
        document.getElementById(id).classList.add("selected");
        this.shopNameSelected = name;
        this.selectedId = id;
      }
      console.log(this.shopNameSelected);
    },
    /**
     * Sự kiến nhấn đúp vào 1 hàng
     * Create By: TXTrinh (22/02/2021)
     */
    rowOnDBClick(id){
      this.isHideParent = false;
      this.title = "Cập nhập cửa hàng";
      EventBus.$emit('showShop', id);
    },
    /**
     * Đóng modal dialog
     * Create By: TXTrinh (22/02/2021)
     */
    closePopup(isHide){
      this.isHideDel = isHide;
      this.isHideParent = isHide;
    },

    /**
     * Các hàm thay đổi startPoint để phân trang
     * Create By: TXTrinh (22/02/2021)
     */
    // Next Page
    IncreasePageNumber(){
        if(this.startPoint == parseInt(this.shopDataLength/this.number)) return;
        this.startPoint++;
        this.SearchShop();
    },
    // Previous Page
    DecreasePageNumber(){
        if(this.startPoint == 0) return;
        this.startPoint--;
        this.SearchShop();
    },
    // First Page
    FirstPageNumber(){
        if(this.startPoint == 0) return;
        this.startPoint = 0;
        this.SearchShop();
    },
    // Last Page
    LastPageNumber(){
        if(this.startPoint == parseInt(this.shopDataLength/this.number)) return;
        this.startPoint = parseInt(this.shopDataLength/this.number);
        if(this.startPoint*this.number == this.shopDataLength) this.startPoint--;
        this.SearchShop();
    },
    
    /**
     * Tìm kiếm cửa hàng theo mã, tên, địa chỉ, số điện thoại ,trạng thái trong DB
     * Create By: TXTrinh (22/02/2021)
     */
    SearchShop(){
        this.isLoading = true;

        let ShopCode, ShopName, Address, PhoneNumber, StatusId, isNull = true;
        this.currentPage = this.startPoint + 1;
        ShopCode = this.txtSearchShopCode
        ShopName = this.txtSearchShopName;
        Address = this.txtSearchAddress;
        PhoneNumber = this.txtSearchPhoneNumber;
        StatusId = this.txtSearchStatus;
        let query = "http://localhost:52698/api/v1/shops/FilterShop?"
        if(ShopCode != null && ShopCode != "") {query += "ShopCode=" + ShopCode; isNull = false};
        if(ShopName != null && ShopName != "") {
          if(!isNull) query += "&ShopName=" + ShopName;
          else{query += "ShopName=" + ShopName; isNull = false}
        };
        if(Address != null && Address != "") {
          if(!isNull) query += "&Address=" + Address;
          else{query += "Address=" + Address; isNull = false}
        };
        if(PhoneNumber != null && PhoneNumber != "") {
          if(!isNull) query += "&PhoneNumber=" + PhoneNumber;
          else{query += "PhoneNumber=" + PhoneNumber; isNull = false}
        };
        if(StatusId != null && StatusId != "") {
          if(!isNull) query += "&StatusId=" + StatusId;
          else{query += "StatusId=" + StatusId; isNull = false}
        };
        axios
            .get(query)
            .then(response => {
                this.shopDataLength = response.data.length;
                this.startListShop = this.number*this.startPoint;
                this.finishListShop = this.number*(this.startPoint + 1);
                this.shops = response.data.slice(this.startListShop, this.finishListShop);
                this.totalPage = Math.ceil(this.shopDataLength/this.number);

                this.isLoading = false;
            })
            .catch(error => {
                console.log(error)
                this.errored = true
            })
            .finally(() => this.loading = false);    
    },
    /**
     * Lọc dữ liệu theo Pages
     * Create By: TXTrinh (22/02/2021)
     */
    SetCurrentPage(){
      this.startPoint = this.currentPage - 1;
      this.SearchShop();
    }
  },
  /**
   * Theo dõi thay đổi của biến number
   * Create By: TXTrinh (22/02/2021)
   */
  watch: {
        number: function() {
            this.SearchShop();
        }
    },
  /**
   * Load dữ liệu ngay khi truy cập
   * Create By: TXTrinh (22/02/2021)
   */
  async created() {
    this.isLoading = true;

    await axios.get("http://localhost:52698/api/v1/shops")
    .then(response => {
      this.shops = response.data.slice(this.startPoint, this.number);
      this.currentPage = this.startPoint + 1;
      this.shopDataLength = response.data.length;
      this.startListShop = this.number*this.startPoint + 1;
      this.finishListShop = this.number*(this.startPoint + 1);
      this.totalPage = Math.ceil(this.shopDataLength/this.number);

      this.isLoading = false;
    })
    .catch(error => {
        console.log(error);
        this.errored = true;
    })
    .finally(() => this.loading = false); 
  },
};
</script>

<style scoped>
</style>