<template>
  <div class="search-input-container">
    <input type="search" placeholder="我還想查詢.." />
    <img
      src="data:image/svg+xml,%3csvg%20width='24'%20height='24'%20viewBox='0%200%2024%2024'%20fill='none'%20xmlns='http://www.w3.org/2000/svg'%3e%3cpath%20d='M11%2019C15.4183%2019%2019%2015.4183%2019%2011%2019%206.58172%2015.4183%203%2011%203C6.58172%203%203%206.58172%203%2011%203%2015.4183%206.58172%2019%2011%2019Z'%20stroke='%23008E6A'%20stroke-width='2'%20stroke-linecap='round'%20stroke-linejoin='round'/%3e%3cpath%20d='M21.0004%2021L16.6504%2016.65'%20stroke='%23008E6A'%20stroke-width='2'%20stroke-linecap='round'%20stroke-linejoin='round'/%3e%3c/svg%3e"
    />
  </div>
</template>
<style>
.search-input-container {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 0px auto;
  width: 50%;
  padding: 0px 0.2vw;
  height: 30px;
  background-color: #fff;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
  border: #ccc solid 2px;
  transition: border-color 0.3s ease-in-out;

  &:focus-within {
    border: #05bf90 solid 2px;
  }

  input {
    all: unset;
    width: 100%;
    height: 100%;
    padding: 0 0.5vw;
    border: none;
    border-radius: 5px;
    font-size: 1vw;
  }

  img {
    height: 20px;
    margin-left: 10px;
    cursor: pointer;
  }

  @media screen and (max-width: 840px) {
    width: 80%;

    input {
      font-size: 2vw;
    }
  }
}
</style>
