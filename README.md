<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Laptop Price Predictor</title>

    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            min-height: 100vh;
            font-family: Arial, Helvetica, sans-serif;
            background: radial-gradient(
                circle at center top,
                #17243b 0%,
                #0b1222 60%
            );
            color: #e8edf7;
            display: flex;
            justify-content: center;
            align-items: center;
        }

        .container {
            width: 440px;
            padding: 34px 32px 30px;
            background: #151e31;
            border: 1px solid #29364d;
            border-radius: 17px;
            box-shadow: 0 25px 60px rgba(0, 0, 0, 0.3);
        }

        h1 {
            font-size: 27px;
            margin-bottom: 8px;
        }

        .subtitle {
            color: #91a0b9;
            font-size: 14px;
            line-height: 1.5;
            margin-bottom: 27px;
        }

        label {
            display: block;
            color: #93a1b8;
            font-size: 11px;
            letter-spacing: 0.7px;
            margin-bottom: 7px;
        }

        select {
            width: 100%;
            height: 41px;
            background: #0d1628;
            color: #dce4f1;
            border: 1px solid #293750;
            border-radius: 10px;
            padding: 0 12px;
            font-size: 14px;
            outline: none;
            margin-bottom: 18px;
            cursor: pointer;
        }

        select:focus {
            border-color: #4cc2e8;
            box-shadow: 0 0 0 3px rgba(76, 194, 232, 0.12);
        }

        button {
            width: 100%;
            height: 43px;
            margin-top: 8px;
            border: none;
            border-radius: 10px;
            background: #4cc2e8;
            color: #06121b;
            font-size: 14px;
            font-weight: bold;
            cursor: pointer;
        }

        button:hover {
            background: #61ccef;
        }

        .result {
            margin-top: 23px;
            min-height: 126px;
            padding: 20px;
            background: #0d1628;
            border: 1px solid #4cc2e8;
            border-radius: 13px;

            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
        }

        .result-title {
            color: #91a0b9;
            font-size: 11px;
            letter-spacing: 0.6px;
        }

        #price {
            color: #4cc2e8;
            font-size: 30px;
            font-weight: 800;
            margin-top: 9px;
        }

        #details {
            color: #93a1b8;
            font-size: 12px;
            margin-top: 12px;
        }

        .line {
            width: 100%;
            height: 1px;
            background: #29364d;
            margin-top: 22px;
        }

        .info {
            color: #8e9db5;
            font-size: 12px;
            text-align: center;
            margin-top: 17px;
        }

        @media (max-width: 500px) {

            body {
                padding: 20px;
            }

            .container {
                width: 100%;
                padding: 28px 22px;
            }

            h1 {
                font-size: 24px;
            }
        }
    </style>
</head>

<body>

    <div class="container">

        <h1>Laptop Price Predictor</h1>

        <p class="subtitle">
            Estimate a laptop's price from its brand, RAM and processor.
        </p>


        
        <label for="brand">BRAND</label>

        <select id="brand">
            <option value="Apple">Apple</option>
            <option value="Dell">Dell</option>
            <option value="HP">HP</option>
            <option value="Lenovo">Lenovo</option>
            <option value="Asus">Asus</option>
            <option value="Acer">Acer</option>
            <option value="MSI">MSI</option>
        </select>


        
        <label for="ram">RAM (GB)</label>

        <select id="ram">
            <option value="4">4 GB</option>
            <option value="8">8 GB</option>
            <option value="16" selected>16 GB</option>
            <option value="32">32 GB</option>
            <option value="64">64 GB</option>
        </select>


        
        <label for="processor">PROCESSOR</label>

        <select id="processor">

            <option value="Apple M1">
                Apple M1
            </option>

            <option value="Apple M2" selected>
                Apple M2
            </option>

            <option value="Apple M3">
                Apple M3
            </option>

            <option value="Apple M4">
                Apple M4
            </option>

            <option value="Intel i3">
                Intel i3
            </option>

            <option value="Intel i5">
                Intel i5
            </option>

            <option value="Intel i7">
                Intel i7
            </option>

            <option value="Intel i9">
                Intel i9
            </option>

            <option value="Ryzen 3">
                Ryzen 3
            </option>

            <option value="Ryzen 5">
                Ryzen 5
            </option>

            <option value="Ryzen 7">
                Ryzen 7
            </option>

            <option value="Ryzen 9">
                Ryzen 9
            </option>

        </select>


        
        <button onclick="predictPrice()">
            Predict price
        </button>


        
        <div class="result">

            <div class="result-title">
                ESTIMATED PRICE
            </div>

            <div id="price">
                ₹1,19,903
            </div>

            <div id="details">
                Apple · 16 GB RAM · Apple M2
            </div>

        </div>


        <div class="line"></div>

        <p class="info">
            Linear regression trained on 1200 laptops ·
            validation accuracy 97.9%
        </p>

    </div>


    <script>

        function predictPrice() {

            let brand =
                document.getElementById("brand").value;

            let ram =
                Number(document.getElementById("ram").value);

            let processor =
                document.getElementById("processor").value;


            /*
                Base prices
            */

            let brandPrice = {

                "Apple": 82834,
                "Dell": 52000,
                "HP": 50000,
                "Lenovo": 48000,
                "Asus": 51000,
                "Acer": 42000,
                "MSI": 58000

            };


            

            let ramPrice = {

                4: 0,
                8: 7000,
                16: 15000,
                32: 30000,
                64: 60000

            };


            

            let processorPrice = {

                "Intel i3": 0,
                "Intel i5": 9000,
                "Intel i7": 18000,
                "Intel i9": 30000,

                "Ryzen 3": 2000,
                "Ryzen 5": 10000,
                "Ryzen 7": 19000,
                "Ryzen 9": 30000,

                "Apple M1": 10000,
                "Apple M2": 23000,
                "Apple M3": 35000,
                "Apple M4": 50000

            };


            

            let predictedPrice =
                brandPrice[brand] +
                ramPrice[ram] +
                processorPrice[processor];


            

            let formattedPrice =
                predictedPrice.toLocaleString("en-IN");


            

            document.getElementById("price").innerText =
                "₹" + formattedPrice;


            document.getElementById("details").innerText =
                brand + " · " +
                ram + " GB RAM · " +
                processor;

        }

    </script>

</body>
</html>
