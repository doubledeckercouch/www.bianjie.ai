<template>
    <div
        class="theme-container"
    >
        <!-- 百度站长 logo -->
        <img class="logo web_logo" src="../assets/link_logo.jpg" alt="边界智能logo">
        <img class="logo web_logo_mobile" src="../assets/link_logo_mobile.jpg" alt="边界智能mobile_logo">
        <ClientOnly>
            <Navigation></Navigation>
        </ClientOnly>
        <ClientOnly>
            <div class="main_container">
                <NewHome v-if="$page.frontmatter.isNewHome"></NewHome>
                <Irita v-if="$page.frontmatter.isIrita"></Irita>
                <Nft v-if="$page.frontmatter.isNft"></Nft>
                <IritaHub v-if="$page.frontmatter.isIritaHub"></IritaHub>
                <IritaOpb v-if="$page.frontmatter.isIritaOpb"></IritaOpb>
                <IritaOpbExtension v-if="$page.frontmatter.isIritaOpbExtension"></IritaOpbExtension>
                <IritaBean v-if="$page.frontmatter.isIritaBean"></IritaBean>
                <IritaDa v-if="$page.frontmatter.isIritaDa"></IritaDa>
                <Dynamic v-if="$page.frontmatter.isDynamic"></Dynamic>
                <Partner v-if="$page.frontmatter.isPartner"></Partner>
                <About v-if="$page.frontmatter.isAbout"></About>
                <Milestone v-if="$page.frontmatter.isMilestone"></Milestone>
                <Honour v-if="$page.frontmatter.isHonour"></Honour>
                <Join v-if="$page.frontmatter.isJoin"></Join>
                <AppScenes v-if="showApp"></AppScenes>
                <Contact></Contact>
                <Markdown :showMd="showMd"></Markdown>
            </div>
        </ClientOnly>

        <ClientOnly>
            <Footer></Footer>
        </ClientOnly>
    </div>
</template>

<script>
import Navigation from "@theme/components/Navigation.vue";
import NewHome from "@theme/components/Home/NewHome.vue";
import Irita from "@theme/components/Product/Irita/Irita.vue";
import Nft from "@theme/components/Product/Nft/Nft.vue";
import IritaHub from "@theme/components/Product/IritaHub.vue";
import IritaOpb from "@theme/components/Product/IritaOpb.vue";
import IritaOpbExtension from "@theme/components/Product/IritaOpbExtension.vue";
import IritaBean from "@theme/components/Product/IritaBean.vue";
import IritaDa from "@theme/components/Product/IritaDa.vue";
import Dynamic from "@theme/components/Dynamic/Dynamic.vue";
import Partner from "@theme/components/Partner/Partner.vue";
import About from "@theme/components/About/About.vue";
import Milestone from "@theme/components/Milestone/Milestone.vue";
import Honour from "@theme/components/Honour/Honour.vue";
import Join from "@theme/components/Join/Join.vue";
import Markdown from "@theme/components/Common/Markdown.vue";
import AppScenes from "@theme/components/AppScenes/AppScenes.vue";
import Footer from "@theme/components/Footer.vue";
import Contact from "@theme/components/Contact.vue";
import cfg from "../../config.json";
import { getCurrentEditionPrefix, getLocalesNav } from '../util';
import { SEO_META } from '../constants';

export default {
    name: "Layout",
    data() {
        return {
            editionPrefix: getCurrentEditionPrefix()
        }
    },
    computed: {
        showMd() {
            return Object.keys(this.$page.frontmatter).length === 0;
        },
        showApp(){
            if(this.$route.path.toLowerCase().includes('e-licence')) {
                return '$page.frontmatter.isELicence';
            }
            if(this.$route.path.toLowerCase().includes('trade-finance')) {
                return '$page.frontmatter.isTradeFinance';
            }
            if(this.$route.path.toLowerCase().includes('c-trading')) {
                return '$page.frontmatter.isCTrading';
            }
            if(this.$route.path.toLowerCase().includes('digital-art')) {
                return '$page.frontmatter.isDigitalArt';
            }
            if(this.$route.path.toLowerCase().includes('e-prescription-circulation')) {
                return '$page.frontmatter.isEPC';
            }
            if(this.$route.path.toLowerCase().includes('datacollection')) {
                return '$page.frontmatter.isDataCollection';
            }
            if(this.$route.path.toLowerCase().includes('finance-trade')) {
                return '$page.frontmatter.isFinanceTrade';
            }
        },

    },
    methods: {
        setHeadMeta(lang) {
            SEO_META[this.editionPrefix][lang].forEach(item => {
                const metaList = document.getElementsByTagName('meta');
                const metaNameList = Array.from(metaList).map(metaItem => metaItem.name);
                if(!metaNameList.includes(item.nameValue)) {
                    const metaDom = document.createElement('meta');
                    metaDom[item.name] = item.nameValue;
                    metaDom[item.content] = item.contentDesc;
                    document.getElementsByTagName('head')[0].appendChild(metaDom);
                } else {
                    if(item.nameValue === 'keywords') {
                        const matchMeta = document.querySelector(`meta[name=${item.nameValue}]`);
                        matchMeta?.setAttribute('content', item.contentDesc);
                    }
                }
            })
        }
    },
    mounted() {
        // 友盟统计添加
        const script = document.createElement("script");
        script.src = `https://s4.cnzz.com/z_stat.php?id=${cfg.umengId}&web_id=${cfg.umengWebId}`;
        script.language = "JavaScript";
        document.body.appendChild(script);
        this.setHeadMeta(this.$store.state.currentLang);
    },
    watch: {
        '$route.path': {
            handler(newPath) {
                const nav = getLocalesNav(this, this.$store.state.currentLang);
                nav.forEach((item, index) => {
                    if (item.link === newPath) {
                        this.$store.commit("currentIndex", index);
                    }
                });
            },
            immediate: true,
            deep: true,
        },
        '$store.state.currentLang': {
            handler(newLang) {
                this.setHeadMeta(newLang);
            }
        }
    },
    components: {
        Navigation,
        NewHome,
        Irita,
        Nft,
        IritaHub,
        IritaOpb,
        IritaOpbExtension,
        IritaBean,
        IritaDa,
        Dynamic,
        Partner,
        About,
        Milestone,
        Honour,
        Join,
        Markdown,
        AppScenes,
        Footer,
        Contact,
    },
};
</script>
<style lang='stylus'>
@import '../../public/iconfont/iconfont.css';

.theme-container {
    position: relative;
    display: flex;
    flex-direction: column;
    min-height: 100vh;
    width: 100%;
    height: 100%;

    .main_container {
        flex: 1;
    }
    .web_logo {
        display: none;
    }
    .web_logo_mobile {
        display: none;
    }
}
</style>
