<template>
  <div class="language-switcher">
    <div class="languages-label">{{ $t('test') }}: </div>
    <div class="languages">
      <div
        class="language"
        v-for="el in locales"
        :key="el.code"
        :class="{ active: (el.code === locale) }"
        @click="switchLanguage(el.code)"
      >
        <span>{{ el.name }}</span>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    computed: {
      locales() { return this.$store.state.locales },
      locale() { return this.$store.state.locale }
    },
    methods: {
      switchLanguage (localeCode) {
        document.cookie = `locale=${localeCode}`;
        location.reload();
      }
    }
  }
</script>

<style>
  .language-switcher {
    display: flex;
    padding: 1rem;
  }
  .languages {
    display: flex;
    justify-content: flex-end;
  }

  .language {
    padding-left: .25rem;
    cursor: pointer;
  }
  .language.active {
    text-decoration: underline;
  }

  .language:hover span {
    text-decoration: underline;
  }

  .language:not(:last-child):after {
    content: '|';
    padding-left: .25rem;
  }
</style>
