<template>
    <div @click="checkClick"  ref="invoiceWrap" class="invoice-wrap flex flex-column">
        <form action="" class="invoice-content">
            <h1>New Invoice</h1>

            <!-- Bill from -->
            <div class="bill-from flex flex-column">
                <h4>Bill from</h4>
                <div class="input flex flex-column">
                    <label for="billerStreetAddress">Street Address</label>
                    <input required type="text" id="billerStreetAddress" v-model="billerStreetAddress">
                </div>
                <div class="location-details flex">
                    <div class="input flex flex-column">
                        <label for="billerCity">City</label>
                        <input required type="text" id="billerCity" v-model="billerCity">
                    </div>
                    <div class="input flex flex-column">
                        <label for="billerZipCode">Zip Code</label>
                        <input required type="text" id="billerZipCode" v-model="billerZipCode">
                    </div>
                    <div class="input flex flex-column">
                        <label for="billerCountry">Country</label>
                        <input required type="text" id="billerCountry" v-model="billerCountry">
                    </div>
                </div>
            </div>

            <!-- Bill to -->
            <div class="bill-to flex flex-column">
                <h4>Bill To</h4>
                <div class="input flex flex-column">
                    <label for="clientName">Client's Name</label>
                    <input required type="text" id="clientName" v-model="clientName">
                </div>
                <div class="input flex flex-column">
                    <label for="clientEmail">Client's Email</label>
                    <input required type="text" id="clientEmail" v-model="clientEmail">
                </div>
                <div class="input flex flex-column">
                    <label for="clientStreetAddress">Client's Street Address</label>
                    <input required type="text" id="clientStreetAddress" v-model="clientStreetAddress">
                </div>
                <div class="location-details flex">
                    <div class="input flex flex-column">
                        <label for="clientCity">City</label>
                        <input required type="text" id="clientCity" v-model="clientCity">
                    </div>
                    <div class="input flex flex-column">
                        <label for="clientZipCode">Zip Code</label>
                        <input required type="text" id="clientZipCode" v-model="clientZipCode">
                    </div>
                    <div class="input flex flex-column">
                        <label for="clientCountry">Country</label>
                        <input required type="text" id="clientCountry" v-model="clientCountry">
                    </div>
                </div>
                
            </div>

            <!-- Invoice work details -->
            <div class="invoice-work flex flex-column">
                <div class="payment flex">
                    <div class="input flex flex-column">
                        <label for="invoiceDate">Invoice Date</label>
                        <input required type="text" id="invoiceDate" v-model="invoiceDate">
                    </div>
                    <div class="input flex flex-column">
                        <label for="paymentDueDate">Payment due date</label>
                        <input required type="text" id="paymentDueDate" v-model="paymentDueDate">
                    </div>
                </div>

                <div class="input flex flex-column">
                    <div class="input flex flex-column">
                        <label for="paymentTerms">Payment Terms</label>
                        <select required type="text" id="paymentTerms" v-model="paymentTerms">
                            <option value="30">Next 30 days</option>
                            <option value="60">Next 60 days</option>
                        </select>
                    </div>
                    <div class="input flex flex-column">
                        <label for="productDescription">Product Description</label>
                        <input required type="text" id="productDescription" v-model="productDescription">
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>

<script>

export default {
    name: "invoiceModal",
  data() {
    return {
      dateOptions: { year: "numeric", month: "short", day: "numeric" },
      docId: null,
      loading: null,
      billerStreetAddress: null,
      billerCity: null,
      billerZipCode: null,
      billerCountry: null,
      clientName: null,
      clientEmail: null,
      clientStreetAddress: null,
      clientCity: null,
      clientZipCode: null,
      clientCountry: null,
      invoiceDateUnix: null,
      invoiceDate: null,
      paymentTerms: null,
      paymentDueDateUnix: null,
      paymentDueDate: null,
      productDescription: null,
      invoicePending: null,
      invoiceDraft: null,
      invoiceItemList: [],
      invoiceTotal: 0,
    };
  },

  components: {


  },


}
</script>

<style lang="scss" scoped>
.invoice-view {
  .nav-link {
    margin-bottom: 32px;
    align-items: center;
    color: #fff;
    font-size: 12px;
    img {
      margin-right: 16px;
      width: 7px;
      height: 10px;
    }
  }

  .header,
  .invoice-details {
    background-color: #1e2139;
    border-radius: 20px;
  }

  .header {
    align-items: center;
    padding: 24px 32px;
    font-size: 12px;

    .left {
      align-items: center;

      span {
        color: #dfe3fa;
        margin-right: 16px;
      }
    }

    .right {
      flex: 1;
      justify-content: flex-end;

      button {
        color: #fff;
      }
    }
  }

  .invoice-details {
    padding: 48px;
    margin-top: 24px;

    .top {
      div {
        color: #dfe3fa;
        flex: 1;
      }

      .left {
        font-size: 12px;
        p:first-child {
          font-size: 24px;
          text-transform: uppercase;
          color: #fff;
          margin-bottom: 8px;
        }

        p:nth-child(2) {
          font-size: 16px;
        }

        span {
          color: #888eb0;
        }
      }

      .right {
        font-size: 12px;
        align-items: flex-end;
      }
    }

    .middle {
      margin-top: 50px;
      color: #dfe3fa;
      gap: 16px;

      h4 {
        font-size: 12px;
        font-weight: 400;
        margin-bottom: 12px;
      }

      p {
        font-size: 16px;
      }

      .bill,
      .payment {
        flex: 1;
      }

      .payment {
        h4:nth-child(3) {
          margin-top: 32px;
        }

        p {
          font-weight: 600;
        }
      }

      .bill {
        p:nth-child(2) {
          font-size: 16px;
        }
        p:nth-child(3) {
          margin-top: auto;
        }

        p {
          font-size: 12px;
        }
      }

      .send-to {
        flex: 2;
      }
    }

    .bottom {
      margin-top: 50px;

      .billing-items {
        padding: 32px;
        border-radius: 20px 20px 0 0;
        background-color: #252945;

        .heading {
          color: #dfe3fa;
          font-size: 12px;
          margin-bottom: 32px;

          p:first-child {
            flex: 3;
            text-align: left;
          }

          p {
            flex: 1;
            text-align: right;
          }
        }

        .item {
          margin-bottom: 32px;
          font-size: 13px;
          color: #fff;

          &:last-child {
            margin-bottom: 0;
          }

          p:first-child {
            flex: 3;
            text-align: left;
          }

          p {
            flex: 1;
            text-align: right;
          }
        }
      }

      .total {
        color: #fff;
        padding: 32px;
        background-color: rgba(12, 14, 22, 0.7);
        align-items: center;
        border-radius: 0 0 20px 20px;

        p {
          flex: 1;
          font-size: 12px;
        }

        p:nth-child(2) {
          font-size: 28px;
          text-align: right;
        }
      }
    }
  }
}
</style>