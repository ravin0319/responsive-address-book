<template>
    <section class="contact-card">
        <figure>
            <img :src="contact.picture.large" alt="Contact Image" class="contact-card__image" />
        </figure>
        <div class="contact-card__info">

            <div class="contact-card__name">
                <h3>{{ contact.name.first }} {{ contact.name.last }}</h3>
            </div>

            <p class="contact-card__address">
                {{ contact.location.street.number }} {{ contact.location.street.name }}
                <br>
                {{ contact.location.city }}
                <br>
                <span>{{ contact.location.country }}</span>
            </p>
            <div class="contact-card__phone">
                <button class="contact-card__phone-button">Call {{ contact.phone }}</button>
            </div>
        </div>
    </section>
</template>

<script>
export default {
    props: {
        contact: {
            type: Object,
            required: true
        }
    }
};
</script>

<style lang="scss" scoped>
.contact-card {
    display: flex;
    align-items: center;
    padding: 20px 40px;
    border-radius: 12px;
    background-color: #ffffff;
    box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
    transition: transform 0.3s ease;

    &:hover {
        transform: translateY(-5px);
    }

    figure {
        margin: 0;
        height: 100%;
    }

    &__image {
        width: 128px;
        height: 128px;
        border-radius: 50%;
        object-fit: cover;
    }

    &__info {
        text-align: center;
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: space-between;

        h3 {
            font-size: 28px;
            font-weight: 400;
            margin: 0 0 20px 0;
        }

        p {
            margin: 0 0 20px 0;
            font-size: 0.9rem;
            color: #555;
        }

        span {
            text-transform: uppercase;
        }
    }

    .contact-card__phone-button {
        width: 100%;
        height: 30px;
        background-image: linear-gradient(#EF8100, #C47600);
        font-weight: bold;
        font-size: 16px;
        color: #fff;
        border-radius: 6px;
        display: flex;
        align-items: center;
        justify-content: center;
        cursor: pointer;
        border: none;
        outline: none;
    }

    @media (max-width: 430px) {
        flex-direction: column;
        align-items: center;

        &__image {
            margin-bottom: 32px;
        }
    }

    @media (min-width: 431px) and (max-width: 640px) {
        flex-direction: column;
    }

    @media (max-width: 640px) {
        figure {
            height: unset;
        }

        img {
            margin-bottom: 32px;
        }
    }

    @media (min-width: 641px) {
        column-gap: 40px;

        &__info {
            flex-wrap: wrap;
            flex-direction: unset;
            justify-content: unset;
        }

        h3 {
            text-align: left;
            margin: 0;
        }

        .contact-card__name {
            flex-basis: 100%;
            display: flex;
            align-items: flex-end;
            height: 80px;
            margin-bottom: 20px;
        }

        .contact-card__address {
            flex-basis: 50%;
            text-align: left;
            padding-right: 20px;
            box-sizing: border-box;
            margin-bottom: 0;
        }

        .contact-card__phone {
            flex-basis: 50%;
            display: flex;
            justify-content: center;
            align-items: end;
        }
    }
}
</style>