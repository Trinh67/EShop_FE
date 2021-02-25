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
                        :class="{requireErr: !isHideErrorPhone}"
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
                    <option value="">Hà Nội</option>
                    <option value="">Thanh Hóa</option>
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
                    <option value="">Cầu Giấy</option>
                    <option value="">Ba Đình</option>
                    <option value="">Tây Hồ</option>
                    <option value="">Bắc Từ Liêm</option>
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
                    <option value="">Trung Văn</option>
                    <option value="">Mai Dịch</option>
                    <option value="">Cổ Nhuế</option>
                    <option value="">Dịch Vọng</option>
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
import '@/styles/dialog/dialog.scss';
import { EventBus } from '@/EventBus.js'
export default {
  data() {
    return {
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
      // Message
      Alert: {
        Text: "",
        Success: false,
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
        this.Alert.Success = false;
        this.Alert.Text = 'Bạn phải điền thông tin đúng định dạng';
        this.$emit("hanldeAlert", this.Alert);
      }
      else{
        axios.post("http://localhost:52698/api/v1/shops", this.ShopData)
        .then(response => {
            this.btnCancelOnClick(); 
            this.Alert.Success = true;
            this.Alert.Text = response.data['userMsg'];
            this.$emit("hanldeAlert", this.Alert);
            setTimeout(() =>{this.$emit('reload');}, 1000) 
        })
        .catch(error => {
            this.Alert.Success = false;
            this.Alert.Text = error.response.data['userMsg'];
            this.$emit("hanldeAlert", this.Alert);
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
        this.Alert.Success = false;
        this.Alert.Text = 'Bạn phải điền thông tin đúng định dạng';
        this.$emit("hanldeAlert", this.Alert);
      }
      else{
        axios.put("http://localhost:52698/api/v1/shops", this.ShopData)
        .then(response => {
            this.btnCancelOnClick();
            this.Alert.Success = true;
            this.Alert.Text = response.data['userMsg'];
            this.$emit("hanldeAlert", this.Alert);
            setTimeout(() =>{this.$emit('reload');}, 1000) 
        })
        .catch(error => {
            this.Alert.Text = error.response.data['userMsg'];
            this.$emit("hanldeAlert", this.Alert);
        })
      }
    },
    /**
     * Hàm Validate định dạng dữ liệu nhập vào, return: True - hợp lệ; False: không hợp lệ
     * Created by: TXTrinh (22/02/2021)
     *  */ 
    validate(type) {
      const formShopCode = /^[A-Z0-9]{6}$/;
      //const formPhoneVn = /((09|03|07|08|05)+([0-9]{8})\b)/g;
      const formPhoneUs = /^\([0-9]{3}\) [0-9]{3}-[0-9]{4}$/;
      
      switch (type) {
        case 'shopCode':  
          // Validate ShopCode:
          { if((this.ShopData.shopCode == null) || (formShopCode.test(this.ShopData.shopCode.trim())==false) || (this.ShopData.shopCode.trim()=='')) {
            this.isHideErrorCode = false;
          }
          else {
            this.isHideErrorCode = true;
          }
          break;}
        case 'shopName':
          // Validate ShopName: 
          {if ((this.ShopData.shopName == null) || (this.ShopData.shopName.trim() == "")) {
            this.isHideErrorName = false;
          } 
          else {
            this.isHideErrorName = true;
          }
          break;}
        case 'address':
          { 
            // Validate Address:
            if((this.ShopData.address == null) || (this.ShopData.address.trim() == "")) {
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
            if((this.ShopData.phoneNumber != null) && (formPhoneUs.test(this.ShopData.phoneNumber.trim())==false) && (this.ShopData.phoneNumber.trim()!='')) {
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
    /**
     * Kiểm tra toàn bộ dữ liệu
     * Created by: TXTrinh (22/02/2021)
     */
    validateData(){
      this.validate('shopCode');
      this.validate('shopName');
      this.validate('address');
      this.validate('phoneNumber');
      // nếu không có lỗi thì không hiện cảnh báo
      if(this.isHideErrorCode && this.isHideErrorName && this.isHideErrorAddress && this.isHideErrorPhone)
        return true;
      return false;
    },
  },
  /**
   * Khởi tạo giá trị mặc định
   * Created by: TXTrinh (22/02/2021)
   */
  created(){
    this.ShopData = this.Shop;
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
</style>