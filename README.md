# CPP_report_final

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>人感センサー×SNS</title>
    <script src="https://unpkg.com/obniz@3.x/obniz.js"></script>
  </head>
  <body>
    <h3>Connect From Your Browser</h3>
    <script src="./code.js"></script>
  </body>

<script>
const EVENT = "test";
const KEY = "dbFfkTCsV-NgB_nLszGfFq";

let obniz = new Obniz("OBNIZ_ID_HEAR");

obniz.onconnect = async () => {
  const sensor = obniz.wired("Keyestudio_PIR", {
    signal: 0,
    vcc: 1,
    gnd: 2
  });
  sensor.onchange = async val => {
    console.log(val ? "Moving!" : "Stopped");
    if (val)
      await fetch(`https://maker.ifttt.com/trigger/${EVENT}/with/key/${KEY}`);
  };
};   
</script>

</html>
