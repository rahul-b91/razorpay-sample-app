<template>
  <div class="container">
    <div class="row">
      <button @click="makePayment">Pay</button>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {};
  },
  methods: {
    makePayment(e) {
      let rzp1 = new Razorpay(this.createObj());
      rzp1.on("payment.failed", function (response) {
        alert(response.error.code);
        alert(response.error.description);
        alert(response.error.source);
        alert(response.error.step);
        alert(response.error.reason);
        alert(response.error.metadata.order_id);
        alert(response.error.metadata.payment_id);
      });

      rzp1.open();
      e.preventDefault();
    },
    createObj() {
      return {
        key: "rzp_test_buSe3lz98IWBl7", // Enter the Key ID generated from the Dashboard
        // Amount is in currency subunits. Default currency is INR. Hence, 50000 refers to 50000 paise
        amount: "5000",
        name: "card91",
        description: "Pay to card91",
        image: "https://i.ibb.co/rtvCt6d/cardgf.png",
        order_id: "order_HTdVtD0tJCQDUF", //This is a sample Order ID. Pass the `id` obtained in the response of Step 1
        handler: function (response) {
          alert(response.razorpay_payment_id);
          alert(response.razorpay_order_id);
          alert(response.razorpay_signature);
        },
        prefill: {
          name: "Gaurav Kumar",
          email: "gaurav.kumar@example.com",
          contact: "9999999999",
        },
        notes: {
          address: "Razorpay Corporate Office",
        },
        theme: {
          color: "#3399cc",
        },
      };
    },
  },
};
</script>

