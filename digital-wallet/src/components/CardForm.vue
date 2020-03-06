<template>
  <section @input="cardInfo">
    <label for="vendor" class="wideLabel">VENDOR</label>
    <!-- Lagt vandor först för att få valideringen att fungera, om den ligger sist funkar inte funktionen cardInfo() som den ska -->
    <select name id="vendor" v-model="input.vendorInput" @input="validateVendor">
      <option value="bitcoin">BITCOIN INC</option>
      <option value="ninja">NINJA BANK</option>
      <option value="blockchain">BLOCK CHAIN INC</option>
      <option value="evil">EVIL CORP</option>
    </select>
    <label for="cardNrInput" class="wideLabel">
      CARD NUMBER
      <span v-if="cardInput.validNumber" class="error">Valid: Only numbers (16)</span>
    </label>

    <input
      type="text"
      id="cardNrInput"
      placeholder="XXXX XXXX XXXX XXXX"
      v-model="input.nrInput"
      maxlength="16"
      @input="validateNumber"
    />

    <label for="CardNameInput" class="wideLabel">
      CARDHOLDER NAME
      <span v-if="cardInput.validName" class="error">Valid: Firstname Lastname</span>
    </label>

    <input
      type="text"
      id="CardNameInput"
      placeholder="FIRSTNAME LASTNAME"
      v-model="input.nameInput"
      maxlength="22"
      @input="validateName"
    />
    <section class="sides">
      <div class="leftSide">
        <label for="validInput" class="smallLabel">
          VALID THRU
          <span v-if="cardInput.validValid" class="error">Valid: MM/YY</span>
        </label>

        <input
          type="text"
          id="validInput"
          placeholder="XX/XX"
          v-model="input.validInput"
          maxlength="5"
          @input="validateValid"
        />
      </div>
      <div class="rightSide">
        <label for="cvcInput" class="smallLabel">
          CVC
          <span v-if="cardInput.validCvc" class="error">Valid: XXX</span>
        </label>

        <input
          type="text"
          id="cvcInput"
          placeholder="XXX"
          v-model="input.cvcInput"
          maxlength="3"
          @input="validateCvc"
        />
      </div>
    </section>
  </section>
</template>

<script>
export default {
  data: () => {
    return {
      //det du skriver in här skickas upp till addCard och sedan ner till Card för att det du skriver uppdateras i realtid till kortet
      input: {
        nrInput: "",
        nameInput: "",
        validInput: "",
        cvcInput: "",
        vendorInput: "",
        isValid: false
      },
      //för att välja att visa valideringestexten, om false visas den inte.
      cardInput: {
        validNumber: false,
        validName: false,
        validValid: false,
        validCvc: false,
        validVendor: true
      }
    };
  },
  methods: {
    cardInfo() {
      //letar igenom cardInput för att se om alla är true, om false gå vidare till isEmpty
      let isTrue = Object.keys(this.cardInput).every(
        k => this.cardInput[k] == false
      );

      if (isTrue == true) {
        //Letar igenom input för att se om något fält är tomt, om inte är isValid true som på AddCard gör att input sparas.
        let isEmpty = Object.keys(this.input).some(k => this.input[k] === "");
        if (isEmpty == false) {
          this.input.isValid = true;
        }
      }

      this.$emit("cardInfo", this.input);
    },

    validateNumber() {
      if (
        this.checkNumber(this.input.nrInput) == true ||
        this.input.nrInput === ""
      ) {
        this.cardInput.validNumber = false;
      } else {
        this.cardInput.validNumber = true;
      }
    },
    validateName() {
      if (this.checkName(this.input.nameInput) == true) {
        this.cardInput.validName = false;
      } else {
        this.cardInput.validName = true;
      }
    },
    validateValid() {
      if (this.checkValid(this.input.validInput) == true) {
        this.cardInput.validValid = false;
      } else {
        this.cardInput.validValid = true;
      }
    },
    validateCvc() {
      if (this.checkCvc(this.input.cvcInput) == true) {
        this.cardInput.validCvc = false;
      } else {
        this.cardInput.validCvc = true;
      }
    },
    validateVendor() {
      this.cardInput.validVendor = false;
    },
    checkNumber(nrInput) {
      const pattern = /^[0-9]{16}/;
      return pattern.test(nrInput);
    },
    checkName(nameInput) {
      const pattern = /^[a-zA-Z]+ [a-zA-Z]+$/;
      return pattern.test(nameInput);
    },
    checkValid(validInput) {
      const pattern = /^(0[1-9]|1[012])\/\d{2}$/;
      return pattern.test(validInput);
    },
    checkCvc(cvcInput) {
      const pattern = /^[0-9]{3}/;
      return pattern.test(cvcInput);
    }
  }
};
</script>

<style scoped>
::placeholder {
  font-size: 1rem;
  color: black;
  font-family: PT mono;
}

.error {
  font-size: 0.8rem;
  color: red;
  font-family: PT mono;
  margin-left: 0.5rem;
}
.wideLabel {
  font-size: 0.75rem;
  opacity: 0.8;
  width: 24rem;
  display: flex;
}
#cardNrInput,
#CardNameInput,
#vendor {
  width: 24rem;
  height: 3.5rem;
  border: 1px solid rgba(0, 0, 0, 0.8);
  border-radius: 0.5rem;
  background: none;
  padding: 0.5rem 1rem;
  margin: 0 0 1rem 0;
  outline: none;
  font-family: PT mono;
  font-size: 1.1rem;
}

#validInput,
#cvcInput {
  height: 3.5rem;
  border: 1px solid rgba(0, 0, 0, 0.8);
  border-radius: 0.5rem;
  padding: 0.5rem;
  outline: none;
  font-family: PT mono;
  font-size: 1.1rem;
}

.smallLabel {
  font-size: 0.75rem;
  opacity: 0.8;
  text-align: left;
  width: 11rem;
}
.sides {
  display: grid;
  grid-template-columns: 11rem 11rem;

  justify-content: space-between;
  margin: 0 0 1rem 0;
}

.leftSide,
.rightSide {
  display: flex;
  flex-direction: column;
}

.addBtn {
  background-color: black;
  color: white;
}
</style>
