<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <v-card>
        <v-card-title class="headline"> VisibleWoman registry </v-card-title>
        <v-card-text>
          <p>Fill this form to get into the DB</p>
          <v-text-field v-model="payload.Name" label="Name" />
          <v-text-field v-model="payload.Bio" label="Bio" />
          <v-text-field v-model="payload.Pronouns" label="Pronouns" />
          <v-select
            v-model="payload.Genders"
            label="Genders"
            :items="genders"
          />
          <v-select
            v-model="payload.Genres"
            label="Genres"
            :items="genres"
            chips
            multiple
          />
          <v-select
            v-model="payload.Roles"
            label="Roles"
            :items="roles"
            chips
            multiple
          />
          <v-text-field v-model="payload.Twitter" label="Twitter handle" />
          <v-text-field v-model="payload.Instagram" label="Instagram handle" />
          <v-text-field
            v-model="payload.Website"
            :rules="[
              () => !!validateUrl(payload.Website) || 'Provide a valid URL',
            ]"
            label="Your website or portfolio"
          />
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" nuxt @click="submit"> Send </v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>
<script>
export default {
  data() {
    return {
      genders: ['Male', 'Female', 'Non-Binary'],
      genres: [
        'Fantasy',
        'LGBTQ',
        'Manga',
        'Humor',
        'Romance',
        'Drama',
        'Slice of life',
        'Webcomic',
        'Supernatural',
        'Fan art',
      ],
      roles: [
        'Artist',
        'Character Designer',
        'Colorist',
        'Creator',
        'Inker',
        'Penciler',
        'Cartoonist',
        'Cover artist',
      ],
      payload: {
        Name: '',
        Bio: '',
        Pronouns: '',
        Genders: '',
        Instagram: '',
        Twitter: '',
        Genres: [],
        Roles: [],
        Website: '',
      },
    };
  },
  methods: {
    validateUrl(value) {
      return /^(?:(?:(?:https?|ftp):)?\/\/)(?:\S+(?::\S*)?@)?(?:(?!(?:10|127)(?:\.\d{1,3}){3})(?!(?:169\.254|192\.168)(?:\.\d{1,3}){2})(?!172\.(?:1[6-9]|2\d|3[0-1])(?:\.\d{1,3}){2})(?:[1-9]\d?|1\d\d|2[01]\d|22[0-3])(?:\.(?:1?\d{1,2}|2[0-4]\d|25[0-5])){2}(?:\.(?:[1-9]\d?|1\d\d|2[0-4]\d|25[0-4]))|(?:(?:[a-z\u00a1-\uffff0-9]-*)*[a-z\u00a1-\uffff0-9]+)(?:\.(?:[a-z\u00a1-\uffff0-9]-*)*[a-z\u00a1-\uffff0-9]+)*(?:\.(?:[a-z\u00a1-\uffff]{2,})))(?::\d{2,5})?(?:[/?#]\S*)?$/i.test(
        value
      );
    },
    async submit() {
      const webhook =
        'https://hook.integromat.com/1303mb0ix63o1thqx7vylf197yg5ubov';
      await this.$axios.$post(webhook, this.payload);
    },
  },
};
</script>
