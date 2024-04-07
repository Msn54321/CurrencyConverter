# CurrencyConverter
This Repository is made for the Practice of HTML , CSS &amp; JavaScript.
Below is My Javascript Code
-----------------------------------------------------------------------------------------------------------------------------

let URL = `https://api.freecurrencyapi.com/v1/latest?apikey=fca_live_KHjqkVTgI99kVBMvr6FJ5mDqzpNR72SwTcKg3QMy&base_currency=`

const btn = document.querySelector(".btn");
const h5 = document.querySelector("h5");
const selectCountry = document.querySelectorAll(" .country select");

for (select of selectCountry){
    for(currCode in countryWithCodes){
        const countryOption = document.createElement("option");
        countryOption.innerText = currCode;
        countryOption.value = currCode;

        if(select.name === "fromCountry" && currCode === "USD"){
            countryOption.selected = "selected";
        } else if(select.name === "toCountry" && currCode === "INR"){
            countryOption.selected = "selected";
        }

        select.append(countryOption);

    }
    select.addEventListener("change" , (evt) => {
        updateFlag(evt.target)
    })
}


const updateFlag = (element) =>{
    let currCode = element.value;
    let countryCode = countryWithCodes[currCode];
    let newSrc = `https://flagsapi.com/${countryCode}/flat/64.png`
    let img = element.parentElement.querySelector(".flag");
    img.src = newSrc;
}

async function populate(quantity, fromCountry, toCountry){
    const getData = await fetch(`${URL}${fromCountry}`);
    const responseData = await getData.json();
    const toCountryValue = responseData.data[toCountry];
    const rate = quantity * toCountryValue;
    h5.innerText = `${quantity} ${fromCountry} = ${rate} ${toCountry}`
}


btn.addEventListener("click",(event) => {
    event.preventDefault();
    const quantity = document.querySelector("#amtInput").value;
    console.log(quantity);
    const fromCountry = document.querySelector("select[name = 'fromCountry']").value
    console.log(fromCountry);
    const toCountry = document.querySelector("select[name = 'toCountry']").value
    console.log(toCountry);  
    populate(quantity, fromCountry, toCountry)
})
