<template>
  <div class="container">
    <p v-for="n in result">
      {{n}}
    </p>
  </div>
</template>

<style>
.container{
  min-width: 200px;
  min-height: 200px;
  color: black;
}
</style>

<script lang="ts" setup>

interface TargetType {
  param: number;
  limit: number;
  position: boolean;
}

const targets: TargetType[] = [
  {param: 246, limit: 1, position: true},
  {param: 692, limit: 2, position: false},
  {param: 174, limit: 0, position: false},
  {param: 419, limit: 1, position: false},
];
const checkNumber = (strNumber: string, targets: TargetType[]): boolean => {
  for (const target of targets) {
    const strTarget: string = target.param.toString().padStart(3, '0');
    let positionCount = 0;
    let notPositionCount = 0;
    for (let i = 0; i < 3; i++) {
      if (strNumber[i] === strTarget[i]) {
        positionCount++;
      } else if (strTarget.includes(strNumber[i])) {
        notPositionCount++;
      }
    }
    if (target.position && (positionCount !== target.limit || notPositionCount != 0)) {
      return false
    }
    if (!target.position && (notPositionCount !== target.limit || positionCount !== 0)) {
      return false
    }
  }
  return true;
};

const result: string[] = []

for (let i = 0; i <= 999; i++) {
  const iStr: string = i.toString().padStart(3, '0');
  const resNumber = checkNumber(iStr, targets)
  if (resNumber) {
    result.push(iStr)
  }
}

</script>