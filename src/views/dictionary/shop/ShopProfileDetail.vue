<template>
  <div>
  <!-- Dialog -->
    <div
      class="m-dialog dialog-detail"
      title="Dialog"
      :class="{ isHide: isHide }"
    >
      <div class="dialog-modal"></div>
      <!-- Dialog Content -->
      <div class="dialog-content">
      <!-- Dialog Header -->
        <div class="dialog-header">
          <div class="dialog-header-title">{{titleDialog}}</div>
          <div class="dialog-header-close">
            <div 
              v-on:click="btnCancelOnClick"
              tabindex="16">x
            </div>
          </div>
        </div>
      <!-- Dialog Body -->
        <div class="dialog-body">
          <div class="m-row m-flex">
            <div class="el-left m-flex-4">
              <div class="m-row m-flex">
                <div class="m-label m-flex-2">
                  Mã cửa hàng <span class="label-required">*</span>
                </div>
                <div class="m-control m-flex-10">
                  <input
                    id="txtShopCode"
                    ref="shopCode"
                    tabindex="1"
                    required
                    :class="{requireErr: !isHideErrorCode}"
                    type="text"
                    @blur="validate('shopCode')"
                    v-model="ShopData.shopCode"
                  />
                  <small 
                    id="error-code" class="error-msg"
                    :class="{isHide:isHideErrorCode}"
                  >* Không được để trống, chỉ chứa chữ in hoa và số, đúng 6 kí tự</small>
                </div>
              </div>
              <div class="m-flex mg-top-15px">
                <div class="m-label m-flex-2">
                  Tên cửa hàng <span class="label-required">*</span>
                </div>
                <div class="m-control m-flex-10">
                  <input
                    id="txtShopName"
                    ref="shopName"
                    tabindex="2"
                    :class="{requireErr: !isHideErrorName}"
                    type="text"
                    @blur="validate('shopName')"
                    v-model="ShopData.shopName"
                    required
                  />
                  <small 
                    id="error-name" class="error-msg"
                    :class="{isHide:isHideErrorName}"
                  >* Tên cửa hàng không được để trống</small>
                </div>
              </div>
              
              <div class="m-flex mg-top-15px">
                <div class="m-label m-flex-2">
                  Địa chỉ <span class="label-required">*</span>
                </div>
                <div class="m-control m-flex-10">
                  <textarea
                    id="txtAddress"
                    :class="{requireErr: !isHideErrorAddress}"
                    ref="address"
                    tabindex="3"
                    type="text"
                    v-model="ShopData.address"
                    @blur="validate('address')"
                    rows= "8"
                    required
                  />
                  <small 
                    id="error-address" class="error-msg"
                    :class="{isHide:isHideErrorAddress}"
                  >* Địa chỉ cửa hàng không được để trống</small>
                </div>
              </div>

              <div class="m-flex mg-top-15px">
                <div class="m-col">
                  <div class="m-flex">
                    <div class="m-label">
                      Số điện thoại
                    </div>
                    <div class="m-control">
                      <input
                        id="txtPhoneNumber"
                        class="input-required"
                        tabindex="4"
                        type="text"
                        v-model="ShopData.phoneNumber"
                        @blur="validate('phoneNumber')"
                        required
                        style="width: 225px; margin-left: 44px"
                      />
                    </div>
                  </div>
                  <small 
                      id="error-phone" class="error-msg"
                      :class="{isHide:isHideErrorPhone}"
                      >SĐT không đúng định dạng US (***) ***-****
                  </small>
                </div>
                <div class="m-flex mg-left-40px">
                  <div class="m-label">
                    Mã số thuế
                  </div>
                  <div class="m-control mg-left-40px">
                    <input
                      id="txtShopTaxCode"
                      type="text"
                      tabindex="5"
                      required
                      v-model="ShopData.shopTaxCode"
                      style="width: 225px"
                    />
                  </div>
                </div>
                <br/>
              </div>
              <div class="m-flex mg-top-15px">
                <div class="m-label m-flex-3">Quốc gia</div>
                <select
                  id="Country"
                  tabindex="6"
                  class="m-control m-flex-5"
                  v-model="ShopData.countryId"
                  style="width: 124px; margin-right: 372px"
                >
                  <option value="">Việt Nam</option>
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
                    tabindex="7"
                    class="m-control m-flex-7"
                    v-model="ShopData.provinceId"
                    style="width: 252px; margin-left: 6px;"
                  >
                    <option value="">Nhập để tìm kiếm</option>
                    <option value="148ed882-32b8-218e-9c20-39c2f00615e8">Hà Nội</option>
                    <option value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">Thanh Hóa</option>
                  </select>
                </div>
                <div class="m-flex mg-left-30px">
                  <div class="m-label m-flex-4">Quận/Huyện</div>
                  <select
                    id="District"
                    tabindex="8"
                    class="m-control m-flex-7"
                    v-model="ShopData.districtId"
                    style="width: 265px;"
                  >
                    <option value="">Nhập để tìm kiếm</option>
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
                    tabindex="9"
                    class="m-control m-flex-7"
                    v-model="ShopData.wardId"
                    style="width: 276px; margin-left: 6px;"
                  >
                    <option value="">Nhập để tìm kiếm</option>
                    <option value="148ed882-32b8-218e-9c20-39c2f00615e8">Trung Văn</option>
                    <option value="25c6c36e-1668-7d10-6e09-bf1378b8dc91">Mai Dịch</option>
                  </select>
                </div>
                <div class="m-flex mg-left-30px">
                  <div class="m-label m-flex-4" style="padding-left: 4px">Đường phố</div>
                  <input
                    id="Street"
                    type="text"
                    tabindex="10"
                    class="m-control m-flex-7"
                    placeholder="Đường phố"
                    style="width: 270px;"
                  /> 
                </div>
              </div>
            </div>
          </div>
        </div>
      <!-- Dialog Footer -->
        <div class="dialog-footer">
          <button 
            id="btnHelp" 
            tabindex="12"
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
            tabindex="13"
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
            tabindex="14"
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
            tabindex="15"
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
      // Các biến dùng để validate
      isHideErrorCode: true,
      isHideErrorName: true,
      isHideErrorAddress: true,
      isHideErrorPhone: true,
      display: "none",
      // Form Data
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
  props: ['isHide', 'titleDialog'],
  methods: {
    /**
     * Đóng dialog
     * Created By: TXTrinh (22/02/2021)
     */
    btnCancelOnClick() {
      this.ShopData = this.Shop;
      this.isHideErrorCode = true;
      this.isHideErrorName = true;
      this.isHideErrorAddress = true;
      this.isHideErrorPhone = true;
      this.$emit('closePopup', true)
    },
    /**
     * Lưu mới cửa hàng
     * Created By: TXTrinh (22/02/2021)
     */
    saveShop() {
      // validate dữ liệu trước khi cho phép thêm
      if(this.validateData() == false) {
        // validate ko hop le.
      }
      else{
        axios.post("http://localhost:52698/api/v1/shops", this.ShopData)
        .then(response => {
            alert(response.data['userMsg']);
            this.btnCancelOnClick(); 
            this.$emit('reload');
        })
        .catch(error => {
            alert(error.response.data['userMsg']);
        })
      }
    },
    /**
     * Cập nhập thông tin cửa hàng 
     * Created By: TXTrinh (22/02/2021)
     */
    editShop(){
      // validate dữ liệu trước khi cho phép sửa
      if(this.validateData() == false) {
        // validate ko hop le.
      }
      else{
        axios.put("http://localhost:52698/api/v1/shops", this.ShopData)
        .then(response => {
            alert(response.data['userMsg']);
            this.btnCancelOnClick();
            this.$emit('reload');
        })
        .catch(error => {
            alert(error.response.data['userMsg']);
        })
      }
    },
    // Hàm Validate định dạng dữ liệu nhập vào, return: True - hợp lệ; False: không hợp lệ
    validate(type) {
      const formShopCode = /^[A-Z0-9]{6}$/;
      //const formPhoneVn = /((09|03|07|08|05)+([0-9]{8})\b)/g;
      const formPhoneUs = /^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$/;
      //var failed = 0;
      
      switch (type) {
        case 'shopCode':  
          // Validate ShopCode:
          { if((formShopCode.test(this.ShopData.shopCode.trim())==false) || (this.ShopData.shopCode.trim()=='')) {
            this.isHideErrorCode = false;
          }
          else {
            this.isHideErrorCode = true;
          }
          break;}
        case 'shopName':
          // Validate ShopName: 
          {if ((this.ShopData.shopName == null || this.ShopData.shopName.trim() == "")) {
            this.isHideErrorName = false;
          } 
          else {
            this.isHideErrorName = true;
          }
          break;}
        case 'address':
          { 
            // Validate Address:
            if((this.ShopData.address==null || this.ShopData.address.trim() == "")) {
              this.isHideErrorAddress = false;
            }
            else {
              this.isHideErrorAddress = true;
            }
            break;
          }
        case 'phoneNumber':
          { 
            // Validate PhoneNumber
            if((formPhoneUs.test(this.ShopData.phoneNumber.trim())==false) && (this.ShopData.phoneNumber.trim()!='')) {
              this.isHideErrorPhone = false;
            }
            else {
              this.isHideErrorPhone = true;
            }
            break;
          }
        default:
          { 
            break;
          }
      }
    },
    validateData(){
      this.validate('shopCode');
      this.validate('shopName');
      this.validate('address');
      this.validate('phoneNumber');
      // nếu không có lỗi thì không hiện cảnh báo
      if(this.isHideErrorCode && this.isHideErrorName && this.isHideErrorAddress && this.isHideErrorPhone)
        return true;
      return false;
    }
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
          document.getElementById("txtShopCode").focus();
      })
      .catch(error => {
          console.log(error)
          this.errored = true
      })
      .finally(() => this.loading = false)
      })
    },
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
  font-size: 20px;
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
  height: 712px;
  background-color: #fff;
  left: calc(50% - 325px);
  top: calc(50% - 400px);
}
.dialog-body {
  padding: 0 16px 16px 16px;
}
.dialog-footer {
  display: flex;
  width: 100%;
  height: 68px;
  background-color: #e9ebee;
  border-radius: 0 0 5px 5px;
  align-items: center;
  justify-content: flex-end;
  padding: 12px 24px;
  box-sizing: border-box;
  margin-top: 16px;
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

textarea#txtAddress{
  padding: 16px;
  width: calc(100% - 36px);
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
.error{
  border: 1px solid #FF0000;
}
.error-msg{
  color: #FF0000;
  font-style: italic;
}
#error-phone{
  padding-left: 120px;
}
.requireErr, .require-error:focus{
    border: 1px solid #FF0000 !important;
}
</style>