<template>
  <v-app>
    <v-navigation-drawer app mobile-breakpoint="0" :mini-variant="mini" mini-variant-width="60">
      <v-list-item two-line>
        <v-list-item-avatar>
          <v-tooltip :bottom="!mini" :right="mini">
            <template v-slot:activator="{on, attrs}">
              <v-btn icon v-bind="attrs" v-on="on" href="#">
                <v-icon large>mdi-account-circle</v-icon>
              </v-btn>
            </template>
            <span>You must login first, click to login</span>
          </v-tooltip>
        </v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-subtitle>You are not logged in</v-list-item-subtitle>
          <v-tooltip bottom>
            <template v-slot:activator="{on, attrs}">
              <v-list-item-subtitle v-bind="attrs" v-on="on">
                <a href="#">Go to sign in page</a>
              </v-list-item-subtitle>
            </template>
            <span>This link will direct you to the sign in page</span>
          </v-tooltip>
        </v-list-item-content>
      </v-list-item>
      <v-divider></v-divider>
      <v-list dense nav>
        <v-subheader v-if="!mini">MENU</v-subheader>
        <v-tooltip v-for="(item, index) in menu" :key="index" :bottom="!mini" :right="mini">
          <template v-slot:activator="{on, attrs}">
            <v-list-item link v-bind="attrs" v-on="on" :href="item.href">
              <v-list-item-icon>
                <v-icon>{{ item.icon }}</v-icon>
              </v-list-item-icon>
              <v-list-item-content>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
              </v-list-item-content>
            </v-list-item>
          </template>
          <span>{{ item.tooltip }}</span>
        </v-tooltip>
      </v-list>
      <template v-slot:append>
        <v-list-item>
          <v-list-item-content v-if="!mini">
            <v-list-item-title>
              <v-tooltip right v-for="(item, index) in toolbarMenu" :key="index">
                <template v-slot:activator="{on, attrs }">
                  <v-btn icon @click="item.onClickHandler" v-bind="attrs" v-on="on">
                    <v-icon>{{item.icon}}</v-icon>
                  </v-btn>
                </template>
                <span>{{item.tooltip}}</span>
              </v-tooltip>
            </v-list-item-title>
          </v-list-item-content>
          <v-list-item-avatar>
            <v-btn icon @click="overWriteBreakpoint">
              <v-tooltip right v-if="mini">
                <template v-slot:activator="{on, attrs}">
                  <v-icon large v-bind="attrs" v-on="on">mdi-chevron-right</v-icon>
                </template>
                <span>Expand the drawer</span>
              </v-tooltip>
              <v-tooltip left v-if="$vuetify.breakpoint.smAndDown && !mini">
                <template v-slot:activator="{on, attrs}">
                  <v-icon large v-bind="attrs" v-on="on">mdi-chevron-left</v-icon>
                </template>
                <span>Shrink the drawer</span>
              </v-tooltip>
            </v-btn>
          </v-list-item-avatar>
        </v-list-item>
      </template>
    </v-navigation-drawer>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      overWriteBreakpointVariable: true,
      toolbarMenu: [
        {
          onClickHandler: this.test,
          tooltip: "Click to change theme",
          icon: "mdi-brightness-4",
        },
        {
          onClickHandler: this.test,
          tooltip: "Support on github",
          icon: "mdi-github",
        },
        {
          onClickHandler: this.test,
          tooltip: "Donate",
          icon: "mdi-cash-usd-outline",
        },
      ],
      menu: [
        {
          title: "Followers",
          tooltip: "This menu has the features you want",
          href: "#",
          icon: "mdi-account-group",
        },
        {
          title: "Likes",
          tooltip: "This menu gives you as many likes as you want",
          href: "#",
          icon: "mdi-thumb-up",
        },
        {
          title: "About",
          tooltip: "This menu provides knowledge about this website",
          href: "#",
          icon: "mdi-information",
        },
        {
          title: "Help",
          tooltip: "If you need help, click this icon",
          href: "#",
          icon: "mdi-help-circle",
        },
      ],
    };
  },
  computed: {
    mini: {
      get() {
        if (this.$vuetify.breakpoint.smAndDown) {
          return this.overWriteBreakpointVariable;
        }
        return this.$vuetify.breakpoint.smAndDown;
      },
      set(value) {
        this.overWriteBreakpointVariable = value;
      },
    },
  },
  methods: {
    overWriteBreakpoint() {
      this.overWriteBreakpointVariable = !this.overWriteBreakpointVariable;
    },
    test() {
      console.log("asd");
    },
  },
};
</script>
