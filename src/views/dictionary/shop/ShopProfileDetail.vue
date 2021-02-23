<template>
  <div>
    <div
      class="m-dialog dialog-detail"
      title="Thông tin nhân viên"
      :class="{ isHide: isHide }"
    >
      <div class="dialog-modal"></div>
      <div class="dialog-content">
        <div class="dialog-header">
          <div class="dialog-header-title">Thêm mới/Cập nhập cửa hàng</div>
          <div class="dialog-header-close">
            <div v-on:click="btnCancelOnClick">x</div>
          </div>
        </div>
        <div class="dialog-body">
          <div class="m-row m-flex">
            <div class="m-row el-left m-flex-4">
              <div class="m-row m-flex">
                <div class="m-label m-flex-2">
                  Mã cửa hàng <span class="label-required">*</span>
                </div>
                <div class="m-control m-flex-10">
                  <input
                    id="txtShopCode"
                    fieldName="ShopCode"
                    required
                    class="input-required"
                    type="text"
                    v-model="ShopData.shopCode"
                  />
                </div>
              </div>
              <div class="m-flex mg-top-15px">
                <div class="m-label m-flex-2">
                  Tên cửa hàng <span class="label-required">*</span>
                </div>
                <div class="m-control m-flex-10">
                  <input
                    id="txtShopName"
                    fieldName="ShopName"
                    class="input-required"
                    type="text"
                    v-model="ShopData.shopName"
                    required
                  />
                </div>
              </div>
              
              <div class="m-flex mg-top-15px">
                <div class="m-label m-flex-2">
                  Địa chỉ <span class="label-required">*</span>
                </div>
                <div class="m-control m-flex-10">
                  <textarea
                    id="txtAddress"
                    fieldName="Address"
                    class="input-required"
                    type="text"
                    v-model="ShopData.address"
                    rows= "8"
                    cols= "78"
                    required
                  />
                </div>
              </div>

              <div class="m-flex mg-top-15px">
                <div class="m-flex">
                  <div class="m-label">
                    Số điện thoại
                  </div>
                  <div class="m-control">
                    <input
                      id="txtPhoneNumber"
                      fieldName="ShopName"
                      class="input-required"
                      type="text"
                      v-model="ShopData.phoneNumber"
                      required
                      style="width: 226px; margin-left: 42px"
                    />
                  </div>
                </div>
                <div class="m-flex mg-left-40px">
                  <div class="m-label">
                    Mã số thuế
                  </div>
                  <div class="m-control mg-left-40px">
                    <input
                      id="txtShopTaxCode"
                      fieldName="ShopTaxCode"
                      type="text"
                      required
                      v-model="ShopData.shopTaxCode"
                      style="width: 226px"
                    />
                  </div>
                </div>
              </div>
              <div class="m-flex mg-top-15px">
                <div class="m-label m-flex-3">Quốc gia</div>
                <select
                  id="Country"
                  fieldName="CountryName"
                  fieldValue="CountryId"
                  class="m-control m-flex-5"
                  v-model="ShopData.countryId"
                  style="width: 124px; margin-right: 373px"
                >
                  <option value="">Chọn Quốc gia</option>
                  <option value="6118a7ff-742b-25db-a9c1-8e252c39bb73">Việt Nam</option>
                </select>
              </div>
              <input type="hidden" 
                v-model="ShopData.statusId"
                value="674934cc-42cf-20cf-1d4a-aea48a10ed18"
              />
              <div class="m-row m-flex">
                <div class="m-flex">
                  <div class="m-label m-flex-4">Tỉnh/Thành phố</div>
                  <select
                    id="Province"
                    fieldName="ProvinceName"
                    fieldValue="ProvinceId"
                    class="m-control m-flex-7"
                    v-model="ShopData.provinceId"
                    style="width: 248px; margin-left: 7px"
                  >
                    <option value="">Chọn Tỉnh/Thành phố</option>
                    <option value="148ed882-32b8-218e-9c20-39c2f00615e8">Hà Nội</option>
                    <option value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">Thanh Hóa</option>
                  </select>
                </div>
                <div class="m-flex mg-left-40px">
                  <div class="m-label m-flex-4">Quận/Huyện</div>
                  <select
                    id="District"
                    fieldName="DistrictName"
                    fieldValue="DistrictId"
                    class="m-control m-flex-7"
                    v-model="ShopData.districtId"
                    style="width: 256px;"
                  >
                    <option value="">Chọn Quận/Huyện</option>
                    <option value="148ed882-32b8-218e-9c20-39c2f00615e8">Cầu Giấy</option>
                    <option value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">Bắc Từ Liêm</option>
                  </select>
                </div>
              </div>
              <div class="m-row m-flex">
                <div class="m-flex">
                  <div class="m-label m-flex-4">Phường/Xã</div>
                  <select
                    id="Ward"
                    fieldName="WardName"
                    fieldValue="WardId"
                    class="m-control m-flex-7"
                    v-model="ShopData.wardId"
                    style="width: 269px; margin-left: 10px"
                  >
                    <option value="">Chọn Phường/Xã</option>
                    <option value="148ed882-32b8-218e-9c20-39c2f00615e8">Trung Văn</option>
                    <option value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">Mai Dịch</option>
                  </select>
                </div>
                <div class="m-flex mg-left-40px">
                  <div class="m-label m-flex-4">Đường phố</div>
                  <input
                    id="Street"
                    fieldName="StreetName"
                    type="text"
                    class="m-control m-flex-7"
                    placeholder="Đường phố"
                    style="width: 266px;"
                  /> 
                </div>
              </div>
            </div>
          </div>
        </div>
        <div class="dialog-footer">
          <button 
            id="btnHelp" 
            class="m-btn m-btn-default"
          >
            <div class="items-header icons-support"></div>
            <span 
              class="btn-text" 
            >
              Trợ giúp
            </span>
          </button>
          <button 
            id="btnSave" 
            class="m-btn m-btn-default"
          >
            <div class="btn-toolbar-icon icon-save"></div>
            <span 
              class="btn-text" 
              v-on:click="editShop"
            >
              Lưu
            </span>
          </button>
          <button 
            id="btnSaveAdd" 
            class="m-btn m-btn-default"
          >
            <div class="btn-toolbar-icon icon-add-save"></div>
            <span 
              class="btn-text" 
              v-on:click="saveShop"
            >
              Lưu và thêm mới
            </span>
          </button>
          <button 
            id="btnCancel" 
            class="m-btn m-btn-default m-btn-cancel" 
            v-on:click="btnCancelOnClick"
          >
            <div class="btn-toolbar-icon icon-cancel"></div>
            Hủy bỏ
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import * as axios from "axios";
import { EventBus } from './../../../EventBus.js'
export default {
  data() {
    return {
      dialog: false,
      //isHide: true,
      display: "none",
      ShopData: {},
      Shop: {
        'shopCode': '',
        'shopName': '',
        'address': '',
        'phoneNumber': '',
        'statusId': '674934cc-42cf-20cf-1d4a-aea48a10ed18',
        'countryId': "",
        'provinceId': "",
        'districtId': "",
        'wardId': "",
      },
    };
  },
  props: ['isHide'],
  methods: {
    /**
     * Đóng dialog
     * Created By: TXTrinh (22/02/2021)
     */
    btnCancelOnClick() {
      this.ShopData = this.Shop;
      this.$emit('closePopup', true)
    },
    /**
     * Lưu mới cửa hàng
     * Created By: TXTrinh (22/02/2021)
     */
    async saveShop() {
      await axios.post("http://localhost:52698/api/v1/shops", this.ShopData)
      .then(response => {
          alert(response.data['userMsg']);
          this.btnCancelOnClick(); 
          this.$emit('reload');
      })
      .catch(error => {
          alert(error.response.data['userMsg']);
      })
    },
    /**
     * Cập nhập thông tin cửa hàng 
     * Created By: TXTrinh (22/02/2021)
     */
    async editShop(){
      await axios.put("http://localhost:52698/api/v1/shops", this.ShopData)
      .then(response => {
          alert(response.data['userMsg']);
          this.btnCancelOnClick();
          this.$emit('reload');
      })
      .catch(error => {
          alert(error.response.data['userMsg']);
      })
    },
  },
  /**
   * Lấy thông tin cửa hàng theo Id
   * Created By: TXTrinh (22/02/2021)
   */
  mounted(){
    EventBus.$on('showShop', idShop => {
        axios
        .get('http://localhost:52698/api/v1/shops/' + idShop)
        .then(response => {
            this.ShopData = response.data[0];
        })
        .catch(error => {
            console.log(error)
            this.errored = true
        })
        .finally(() => this.loading = false)
        })
    }
};
</script>
<style scoped>
.isHide {
  display: none;
}
.m-dialog {
  z-index: 3 !important;
}
.dialog-content{
  z-index: 4;
}
.dialog-header {
  position: relative;
  height: 45px;
  line-height: 60px;
  padding-bottom: 16px;
  padding-left: 16px;
  border-radius: 4px;
  display: flex;
  font-size: 24px;
  font-weight: bold;
  background-color: #d8d8d8;
}

.dialog-header-close {
  position: absolute;
  right: 16px;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  color: #a5a5a5;
  cursor: pointer;
  top: 16px;
  align-items: center;
  border: none;
  font-size: 30px;
  line-height: 24px;
}
.dialog-modal {
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: black;
  opacity: 0.4;
  z-index: 3;
}

.dialog-content {
  position: fixed;
  border-radius: 5px;
  width: 750px;
  height: 700px;
  background-color: #fff;
  left: calc(50% - 325px);
  top: calc(50% - 375px);
}
.dialog-body {
  padding: 0 16px 16px 16px;
}
.dialog-footer {
  display: flex;
  width: 100%;
  height: 65px;
  background-color: #e9ebee;
  border-radius: 0 0 5px 5px;
  align-items: center;
  justify-content: flex-end;
  padding: 12px 24px;
  box-sizing: border-box;
  margin-top: 10px;
}
.currency-for-input {
  position: absolute;
  right: 40px;
  line-height: 40px;
  font-style: italic;
}
.dialog-footer button {
  height: 35px;
  width: auto;
  color: #00577b;
  font-weight: bold;
  border-radius: 4px;
  font-size: 16px;
}
.dialog-footer button:hover{
  background-color: #0088c1;
}
.dialog-footer .icons-support{
  margin-top: 0px!important;
}
#btnHelp{
  margin-right: 170px;
  margin-left: 0px;
  padding-left: 0px;
  background-color: #e9ebee;
}
#btnSave{
  color: #ffffff;
}
#btnSaveAdd{
  background-color: #ffffff;
  border: 1px solid #00577b;
}
#btnSaveAdd:hover, #btnCancel:hover{
  color: #ffffff;
  background-color: #0088c1;
}

textarea{
  padding: 16px;
}
select#cbxPosition{
  margin-right: 375px;
}
input, select{
  height: 45px;
}
input:focus, select:focus, textarea:focus{
  border: 1px solid #3ec347!important;
  outline: none!important;
}
</style>