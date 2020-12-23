<template>
  <div class="base-station-card">
    <div>
      <span class="site-name">{{ site.type }}</span>
    </div>
    <div class="card-main-inner">
      <div class="card-header">
        <div class="d-flex justify-between">
          <h2 class="card-title mb-3">Площадка {{ site.name || "..." }}</h2>
          <div>
            <img :src="coverTypeImage" alt="" class="cover-style" />
          </div>
        </div>
        <div class="d-flex justify-between">
          <p class="mb-1">N{{ siteNumber }}{{ streetAndBuilding }}</p>
          <p>{{ longitude }}</p>
        </div>
        <div class="d-flex justify-between">
          <p class="font-thin">{{ regionAndCity }}</p>
          <p>{{ latitude }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import indoorIcon from "@/assets/images/indoor.svg";
import outdoorIcon from "@/assets/images/outdoor.svg";

const SITE_TYPE = "Site";
const BASE_STATION_TYPE = "BaseStation";
const ANTENNA_TYPE = "Antenna_RAN";
const AMC_TYPE = "AMC";

export default {
  name: "BaseStation",

  props: {
    stationData: {
      type: Array,
      required: true,
    },
  },

  computed: {
    site() {
      return this.stationData.find((dataItem) => dataItem.type === SITE_TYPE);
    },
    baseStation() {
      return this.stationData.find(
        (dataItem) => dataItem.type === BASE_STATION_TYPE
      );
    },
    antennas() {
      return this.stationData.filter(
        (dataItem) => dataItem.type === ANTENNA_TYPE
      );
    },
    amc() {
      return this.stationData.find((dataItem) => dataItem.type === AMC_TYPE);
    },
    siteNumber() {
      return (
        this.site.resourceCharacteristic.find(
          (item) => item.name === "siteNumber"
        )?.value ?? "..."
      );
    },
    addressParts() {
      const siteAddress = this.site.resourceCharacteristic.find(
        (item) => item.name === "siteAddress"
      );
      return siteAddress.value.split(",");
    },
    regionAndCity() {
      return `${this.addressParts[0]}, ${this.addressParts[1]}`;
    },
    streetAndBuilding() {
      return `${this.addressParts[2]}, ${this.addressParts[3]}`;
    },
    coverTypeImage() {
      const coverType = this.baseStation.resourceCharacteristic.find(
        (item) => item.name === "coverType"
      )?.value;
      return coverType === "INDOOR" ? indoorIcon : outdoorIcon;
    },
    longitude() {
      return this.site.resourceCharacteristic.find(
        (item) => item.name === "longitude"
      )?.value;
    },
    latitude() {
      return this.site.resourceCharacteristic.find(
        (item) => item.name === "latitude"
      )?.value;
    },
  },
};
</script>

<style scoped>
.base-station-card {
  border: 1px solid #2c2c2c;
}
.card-main-inner {
  padding: 25px 25px 20px;
}
.site-name {
  padding: 10px 16px;
  display: inline-block;
  font-weight: bold;
  background-color: #2c2c2c;
  color: #fff;
}
.card-title {
  font-size: 1.5rem;
  font-weight: bold;
}
.cover-style {
  width: 20px;
  height: 20px;
}
</style>