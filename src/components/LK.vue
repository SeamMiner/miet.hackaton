<template>
<div id="profile">

  <b-container class="mt-5">
    <b-row>
      <b-col cols="12" class="d-flex justify-content-between align-items-center">

        <p class="primaryText">Наслаждайтесь<br>квестами, Александр!</p>

        <b-avatar src="https://sun9-37.userapi.com/impg/c858120/v858120820/15c45c/Z7knSkWXXVw.jpg?size=200x0&quality=90&crop=48,19,264,264&sign=f81b13103a6b3258bf71d01989dd4aff&ava=1"></b-avatar>

      </b-col>

      <b-col cols="12" class="description mt-3">Квесты</b-col>
      <b-col cols="6" class="d-flex flex-column justify-content-between p-2">
        <router-link class="text-decoration-none" to="/competetive">
          <div class="routerLinkProfile cardQuest">
            <b-avatar class="mb-4" src="https://sun9-37.userapi.com/impg/c858120/v858120820/15c45c/Z7knSkWXXVw.jpg?size=200x0&quality=90&crop=48,19,264,264&sign=f81b13103a6b3258bf71d01989dd4aff&ava=1"></b-avatar>

            <p class="primaryTextQuest">Соревнования</p>

            <p class="descriptionQuest mb-0">Состязания команд</p>
          </div>
        </router-link>
      </b-col>

      <b-col cols="6" class="d-flex flex-column justify-content-between p-2">
        <router-link class="text-decoration-none" to="/bestPlaces">
          <div class="routerLinkProfile cardQuest">
            <img class="mb-4" height="40" width="40" src="@/assets/walkingMan.svg" alt="walkingMan">

            <p class="primaryTextQuest">Прогулка</p>

            <p class="descriptionQuest mb-0">Состязания команд</p>
          </div>
        </router-link>
      </b-col>

      <b-col cols="6" class="d-flex flex-column justify-content-between p-2">
        <router-link class="text-decoration-none" to="/geoquestion">
          <div class="routerLinkProfile cardQuest">
            <b-avatar class="mb-4" src="https://sun9-37.userapi.com/impg/c858120/v858120820/15c45c/Z7knSkWXXVw.jpg?size=200x0&quality=90&crop=48,19,264,264&sign=f81b13103a6b3258bf71d01989dd4aff&ava=1"></b-avatar>

            <p class="primaryTextQuest">Геозагадка</p>

            <p class="descriptionQuest mb-0">Мини-квест</p>
          </div>
        </router-link>
      </b-col>

      <b-col cols="6" class="d-flex flex-column justify-content-between p-2">
        <router-link class="text-decoration-none" to="/create">
          <div class="routerLinkProfile cardQuest">
            <img class="mb-4" height="40" width="40" src="@/assets/createQuest.svg" alt="createQuest">

            <p class="primaryTextQuest">Создать квест</p>

            <p class="descriptionQuest mb-0">Состязания команд</p>
          </div>
        </router-link>
      </b-col>

<!--      <b-col cols="12" class="description mt-3">Рекомендация для вас</b-col>-->
<!--      <b-col cols="12" class="p-2">-->
<!--      <div class="cardQuest w-100 d-flex justify-content-between align-items-center">-->
<!--        <div class="topics">-->
<!--          <p class="primaryText">Соревнования</p>-->
<!--          <p class="description mb-0">Состязания команд</p>-->
<!--        </div>-->
<!--        <div class="goTo">-->
<!--          <svg width="20" height="28" viewBox="0 0 20 28" fill="none" xmlns="http://www.w3.org/2000/svg">-->
<!--            <path d="M15.4393 12.9393L6.99998 4.5C6.4477 3.94771 5.55227 3.94771 4.99998 4.5C4.4477 5.05228 4.4477 5.94771 4.99998 6.5L12.5 14L4.99998 21.5C4.4477 22.0523 4.4477 22.9477 4.99998 23.5C5.55227 24.0523 6.4477 24.0523 6.99998 23.5L15.4393 15.0607C16.0251 14.4749 16.0251 13.5251 15.4393 12.9393Z" fill="#3F8AE0"/>-->
<!--          </svg>-->
<!--        </div>-->
<!--        </div>-->
<!--      </b-col>-->

      <b-col cols="12" class="d-flex flex-column justify-content-between p-2">
        <router-link class="text-decoration-none" to="/bestPlaces">
          <div class="routerLinkProfile cardQuest cardBlue w-100">
            <img class="mb-4" src="@/assets/personalQuests.svg" alt="personalQuests">

            <p class="primaryText text-light">Персональный маршрут</p>

            <p class="description text-light mb-3">Найдите для себя что-то новое</p>
          </div>
        </router-link>
      </b-col>

      <b-col cols="12" class="description mt-3">Гео-рисунки</b-col>
      <b-col cols="12" class="d-flex flex-column justify-content-between p-2">
        <router-link class="text-decoration-none" to="/geo-pictures">
          <div class="routerLinkProfile cardQuest w-100">
            <img class="mb-4" src="@/assets/personalQuests.svg" alt="personalQuests">

            <p class="primaryText ">Гео-рисунки</p>

            <p class="description mb-3">Получи за баллы команды гео-рисунки</p>
          </div>
        </router-link>
      </b-col>

    </b-row>
  </b-container>

</div>
</template>

<script>
export default {
  name: "LK"
}
</script>

<style>
.primaryText {
  font-family: SF Pro Text, sans-serif;
  font-style: normal;
  font-weight: 600;
  font-size: 22px;
  line-height: 26px;
  color: #2F2F2F;
}

.description {
  font-family: SF Pro Text, sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 14px;
  line-height: 14px;
  color: #818C99;
  margin-bottom: 24px;
}

.routerLinkProfile {
  transition: all .05s ease-in-out;
}

.routerLinkProfile:hover {
  box-shadow: 0 4px 56px rgba(0, 0, 0, 0.1);
}

.cardQuest {
  background: #FFFFFF;
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.1);
  border-radius: 24px;
  padding: 20px 16px;
}

.primaryTextQuest {
  font-family: TT Commons, sans-serif;
  font-style: normal;
  font-weight: bold;
  font-size: 18px;
  line-height: 18px;
  color: #2F2F2F;
}
.descriptionQuest {
  font-family: SF Pro Text, sans-serif;
  font-style: normal;
  font-weight: 500;
  font-size: 11px;
  line-height: 14px;
  color: #818C99;
}

.cardBlue {
  background: linear-gradient(242.23deg, #A0C7FF -17.6%, #448CF2 67.25%);
}
</style>
