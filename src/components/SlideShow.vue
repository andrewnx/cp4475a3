<template>
    <div class="swiper-container">
        <Swiper :options="swiperOption">
            <div class="swiper-button-next"></div>
            <div class="swiper-button-prev"></div>
            <div class="swiper-pagination"></div>
            <SwiperSlide v-for="slide in slides" :key="slide.id">
                <img class="slide-image" v-if="slide.image" :src="slide.image" :alt="slide.title">
                <div class="slide-text">
                    <h2 class="slide-title">{{ slide.title }}</h2>
                    <p class="section">{{ slide.description }}</p>
                </div>
                <a :href="slide.creditLink" target="_blank" class="credit">Photo by {{ slide.credit }}</a>
            </SwiperSlide>
        </Swiper>
    </div>
</template>

  
  
<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import SwiperCore, { Navigation, Pagination } from 'swiper';
import 'swiper/swiper-bundle.min.css';
import axios from 'axios'

SwiperCore.use([Navigation, Pagination])


export default {
    name: 'SlideShow',
    components: {
        Swiper,
        SwiperSlide
    },
    data() {
        return {
            slides: [],
            swiperOption: {
                navigation: true,
                pagination: {
                    clickable: true
                },
                slidesPerView: 1,
                spaceBetween: 1,
                loop: true,
            }

        }
    },
    async created() {
        const slideInfo = [{
            title: 'Harnessing AI for Website Analysis',
            description: 'In the digital era, AI is becoming a game-changing tool to optimize and analyze websites.AI is a driving force that can revolutionize our approach to website analysis, making it more precise, comprehensive, and dynamic than ever before.'
        },
        {
            title: 'The Role of Website Analysis',
            description: 'Website analysis is a fundamental aspect of digital strategy. It helps us understand user behavior, discover opportunities for improvement, and create an optimal user experience. Effective website analysis directly influences conversion rates and user engagement, underpinning the success of our digital endeavors.'
        },
        {
            title: 'Traditional Approaches to Website Analysis',
            description: 'Traditional methods of website analysis include manual tracking, surveys, and A/B testing. While useful, these methods can be time-consuming and offer limited insights. Traditional approaches often suffer from time constraints, scalability issues, and subjective biases.'
        },
        {
            title: 'Introduction to AI in Website Analysis',
            description: ' Enter Artificial Intelligence, an innovative solution for website analysis. AI brings a new level of automation and intelligence to the analysis process. By leveraging AI, we can gain more accurate insights, take data-driven decisions, and drastically enhance our analysis capabilities.'
        },
        {
            title: 'AI Techniques for Website Analysis',
            description: 'AI employs several techniques in website analysis, such as Natural Language Processing for user feedback analysis, Machine Learning for user segmentation, and Computer Vision for visual content analysis. Each AI technique offers unique insights and benefits, opening new avenues for website analysis and optimization.'
        },
        {
            title: 'Benefits of AI in Website Analysis',
            description: 'AI offers numerous advantages: improved accuracy, in-depth insights through pattern recognition, personalized user experiences, and automation of repetitive tasks. These benefits collectively lead to enhanced website performance and efficient decision-making.'
        },
        {
            title: 'AI-Driven Website Performance Optimization',
            description: 'AI can optimize website performance by analyzing user behavior, identifying improvement areas, automating testing, and offering real-time recommendations. All these capabilities contribute to the creation of a high-performing, user-friendly website.'
        },
        {
            title: 'Practical Application and Examples',
            description: 'Numerous real-world examples demonstrate the successful application of AI in website analysis and optimization. These include renowned tech firms as well as emerging startups. We\'ve seen significant improvements in website performance and user experience due to the integration of AI, as evidenced by tangible before-and-after metrics.'
        },
        {
            title: 'Challenges and Ethical Considerations',
            description: 'Despite its benefits, AI in website analysis also poses certain challenges, such as data quality, algorithm bias, and privacy concerns. It\'s essential to address these challenges and adhere to ethical considerations to ensure responsible usage of AI.'
        },
        {
            title: 'Conclusion',
            description: 'To wrap up, AI brings enormous potential and benefits to website analysis, revolutionizing how we approach optimization and user experience. To stay competitive in the digital landscape, it\'s crucial to embrace AI-powered solutions for website analysis.'
        }];
        const url = 'https://api.unsplash.com/photos/random?count=10&query=technology&orientation=landscape&client_id=qvwhr8VkWQd-RjVQ25sAmegc5eDISh-R7e2SjjLSPKA';
        try {
            const response = await axios.get(url);
            this.slides = await Promise.all(response.data.map(async (photo, index) => {
                const slide = {
                    id: index,
                    image: photo.urls.regular,
                    title: slideInfo[index].title,
                    description: slideInfo[index].description,
                    credit: photo.user.name,
                    creditLink: photo.user.links.html,
                };
                return slide;
            }));
        } catch (err) {
            console.error(err);
        }
    }
}
</script>

<style scoped>
.slide-title {
    margin-bottom: 20px;
}

.section {
    margin-bottom: 10px;
}

.credit {
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 10px;
    background: rgba(0, 0, 0, 0.5);
    color: #fff;
    font-size: 0.8em;
    text-align: center;
    text-decoration: none;
    transition: background 0.3s ease;
}

.credit:hover {
    background: rgba(0, 0, 0, 0.8);
}

.swiper-container {
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 100%;
    flex-grow: 1;
}

.swiper-slide {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    text-align: center;
    position: relative;
}

.slide-image {
    width: 100%;
    height: 50%;
    object-fit: cover;

}

.slide-text {
    position: absolute;
    width: 80%;
    top: 50%;
    left: 50%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    backdrop-filter: blur(10px);
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
    color: #fff;
    overflow: hidden;
    text-overflow: ellipsis;
    transform: translate(-50%, -50%);
    padding: 1em;
}

.swiper-button-next,
.swiper-button-prev,
.swiper-pagination {
    color: #fff;
    background-color: rgba(0, 0, 0, 0.1);
}

@media (max-width: 768px) {
    .slide-text h2 {
        font-size: 1.5em;
    }
}

@media (max-width: 480px) {
    .slide-text h2 {
        font-size: 1.2em;
    }
}
</style>